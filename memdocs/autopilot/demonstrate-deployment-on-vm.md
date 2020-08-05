---
title: Demostración de la implementación de AutoPilot
ms.reviewer: ''
manager: laurawi
description: Instrucciones paso a paso sobre cómo configurar una máquina virtual con una implementación de Windows AutoPilot
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, sin intervención del socio, msfb, Intune, actualización
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom: autopilot
ms.openlocfilehash: 7ff25816c0398389fc23bbde4983f4bc9556d192
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757759"
---
# <a name="demonstrate-autopilot-deployment"></a>Demostración de la implementación de AutoPilot

**Se aplica a**

- Windows 10

Para empezar a trabajar con Windows AutoPilot, debe probarlo con una máquina virtual (VM) o puede usar un dispositivo físico que se borrará y, a continuación, tendrá una instalación nueva de Windows 10.

En este tema aprenderá a configurar una implementación de Windows AutoPilot para una máquina virtual mediante Hyper-V.

> [!NOTE]
> Aunque hay [varias plataformas](add-devices.md#registering-devices) disponibles para habilitar AutoPilot, este laboratorio usa principalmente Intune.

> Hyper-V y una máquina virtual no son necesarios para este laboratorio. También puede usar un dispositivo físico. Sin embargo, las instrucciones suponen que está usando una máquina virtual. Para usar un dispositivo físico, omita las instrucciones para instalar Hyper-V y crear una máquina virtual. Todas las referencias a "dispositivo" en la guía hacen referencia al dispositivo cliente, ya sea físico o virtual.

El vídeo siguiente proporciona información general sobre el proceso:

</br>
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/KYVptkpsOqs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

> Para obtener una lista de los términos usados en esta guía, consulte la sección [Glosario](#glossary) .

## <a name="prerequisites"></a>Prerrequisitos

Estas son las cosas que necesitará para completar este laboratorio:
<table><tr><td>Medios de instalación de Windows 10</td><td>Windows 10 Professional o Enterprise (archivo ISO) para una versión compatible de Windows 10, canal semianual. Si aún no tiene una imagen ISO para usar, se proporciona un vínculo para descargar una <a href="https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise" data-raw-source="[evaluation version of Windows 10 Enterprise](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)">versión de evaluación de Windows 10 Enterprise</a>.</td></tr>
<tr><td>Acceso a Internet</td><td>Si está detrás de un firewall, consulte los <a href="windows-autopilot-requirements.md#networking-requirements" data-raw-source="[networking requirements](windows-autopilot-requirements.md#networking-requirements)">requisitos de red</a>detallados. De lo contrario, solo tiene que asegurarse de que tiene una conexión a Internet.</td></tr>
<tr><td>Hyper-V o un dispositivo físico que ejecuta Windows 10</td><td>En la guía se supone que va a usar una máquina virtual de Hyper-V y proporciona instrucciones para instalar y configurar Hyper-V, si es necesario. Para usar un dispositivo físico, omita los pasos para instalar y configurar Hyper-V.</td></tr>
<tr><td>Una cuenta premium de Intune</td><td>En esta guía se describe cómo obtener una cuenta de evaluación gratuita de 30 días que puede usarse para completar el laboratorio.</td></tr></table>

## <a name="procedures"></a>Procedimientos

A continuación se proporciona un resumen de las secciones y los procedimientos del laboratorio. Siga cada sección en el orden en que se presenta, omitiendo las secciones que no se aplican a usted. En el apéndice se proporcionan procedimientos opcionales.

[Comprobar la compatibilidad de Hyper-V](#verify-support-for-hyper-v)
<br>[Habilitar Hyper-V](#enable-hyper-v)
<br>[Creación de una máquina virtual de demostración](#create-a-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[Establecer la ubicación del archivo ISO](#set-iso-file-location)
<br>&nbsp;&nbsp;&nbsp;[Determinar el nombre del adaptador de red](#determine-network-adapter-name)
<br>&nbsp;&nbsp;&nbsp;  [Usar Windows PowerShell para crear la máquina virtual de demostración](#use-windows-powershell-to-create-the-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[Instalar Windows 10](#install-windows-10)
<br>[Capturar el ID. de hardware](#capture-the-hardware-id)
<br>[Restablecimiento de la máquina virtual a una versión rápida (OOBE)](#reset-the-vm-back-to-out-of-box-experience-oobe)
<br>[Comprobar el nivel de suscripción](#verify-subscription-level)
<br>[Configuración de la personalización de marca de la compañía](#configure-company-branding)
<br>[Configuración de la inscripción automática Microsoft Intune](#configure-microsoft-intune-auto-enrollment)
<br>[Registrar la máquina virtual](#register-your-vm)
<br>&nbsp;&nbsp;&nbsp;[Registro de AutoPilot mediante Intune](#autopilot-registration-using-intune)
<br>&nbsp;&nbsp;&nbsp;[Registro de AutoPilot mediante MSfB](#autopilot-registration-using-msfb)
<br>[Crear y asignar un perfil de implementación de Windows AutoPilot](#create-and-assign-a-windows-autopilot-deployment-profile)
<br>&nbsp;&nbsp;&nbsp;[Creación de un perfil de implementación de Windows AutoPilot mediante Intune](#create-a-windows-autopilot-deployment-profile-using-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Asignar el perfil](#assign-the-profile)
<br>&nbsp;&nbsp;&nbsp;[Crear un perfil de implementación de Windows AutoPilot mediante MSfB](#create-a-windows-autopilot-deployment-profile-using-msfb)
<br>[Consulte Windows AutoPilot en acción](#see-windows-autopilot-in-action)
<br>[Quitar dispositivos del AutoPilot](#remove-devices-from-autopilot)
<br>&nbsp;&nbsp;&nbsp;[Eliminar (Desregistrar) dispositivo AutoPilot](#delete-deregister-autopilot-device)
<br>[Apéndice A: comprobar la compatibilidad de Hyper-V](#appendix-a-verify-support-for-hyper-v)
<br>[Apéndice B: agregar aplicaciones a su perfil](#appendix-b-adding-apps-to-your-profile)
<br>&nbsp;&nbsp;&nbsp;[Agregar una aplicación Win32](#add-a-win32-app)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Preparar la aplicación para Intune](#prepare-the-app-for-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Creación de una aplicación en Intune](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Asignación de la aplicación a su perfil de Intune](#assign-the-app-to-your-intune-profile)
<br>&nbsp;&nbsp;&nbsp;[Agregar Office 365](#add-office-365)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Creación de una aplicación en Intune](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Asignación de la aplicación a su perfil de Intune](#assign-the-app-to-your-intune-profile)
<br>[Glosario](#glossary)

## <a name="verify-support-for-hyper-v"></a>Comprobar la compatibilidad de Hyper-V

Si aún no tiene Hyper-V, primero debemos habilitarlo en un equipo con Windows 10 o Windows Server (2012 R2 o posterior).

> Si ya tiene Hyper-V habilitado, vaya al paso [creación de una máquina virtual de demostración](#create-a-demo-vm) . Si usa un dispositivo físico en lugar de una máquina virtual, vaya a [instalar Windows 10](#install-windows-10).

Si no está seguro de que el dispositivo es compatible con Hyper-V o tiene problemas al instalar Hyper-V, consulte [el apéndice a](#appendix-a-verify-support-for-hyper-v) siguiente para obtener más información sobre cómo comprobar que Hyper-v se puede instalar correctamente.

## <a name="enable-hyper-v"></a>Habilitar Hyper-V

Para habilitar Hyper-V, abra un símbolo del sistema de Windows PowerShell con privilegios elevados y ejecute el siguiente comando:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

Este comando funciona en todos los sistemas operativos compatibles con Hyper-V, pero en los sistemas operativos Windows Server debe escribir un comando adicional (a continuación) para agregar el módulo de Windows PowerShell de Hyper-V y la consola de administrador de Hyper-V. El siguiente comando también instalará Hyper-V si aún no está instalado, por lo que si usa Windows Server, solo tiene que escribir el siguiente comando en lugar de usar el comando enable-WindowsOptionalFeature:

```powershell
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools
```

Cuando se le pida que reinicie el equipo, elija **sí**. Es posible que el equipo se reinicie más de una vez.

> Como alternativa, puede instalar Hyper-V mediante el panel de control de Windows en **activar o desactivar las características de Windows** para un sistema operativo cliente, o mediante el **Asistente para agregar roles y características** de administrador del servidor en un sistema operativo de servidor, como se muestra a continuación:

   ![Característica de Hyper-V](images/hyper-v-feature.png)

   ![Hyper-V](images/svr_mgr2.png)

<P>Si decide instalar Hyper-V mediante Administrador del servidor, acepte todas las selecciones predeterminadas. Asegúrese también de instalar ambos elementos en <strong>Administración de roles Tools\Hyper-V administración de funciones</strong>.

Una vez completada la instalación, abra el administrador de Hyper-V escribiendo **virtmgmt. msc** en un símbolo del sistema con privilegios elevados o escribiendo **Hyper-v** en el cuadro de búsqueda del menú Inicio.

Para obtener más información acerca de Hyper-V, consulte [Introducción a Hyper-v en Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/) e [Hyper-v en Windows Server](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server).

## <a name="create-a-demo-vm"></a>Creación de una máquina virtual de demostración

Ahora que Hyper-V está habilitado, es necesario crear una máquina virtual que ejecute Windows 10. Podemos [crear una máquina](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine) virtual y una [red virtual](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network) mediante el administrador de Hyper-V, pero es más fácil usar Windows PowerShell.

Para usar Windows PowerShell, solo necesitamos saber dos cosas:

1. Ubicación del archivo ISO de Windows 10.
   - En el ejemplo, se supone que la ubicación es **c:\iso\win10-eval.ISO**.
2. El nombre de la interfaz de red que se conecta a Internet.
   - En el ejemplo, usamos un comando de Windows PowerShell para determinarlo automáticamente.

Después de haber establecido la ubicación del archivo ISO y determinado el nombre de la interfaz de red adecuada, podemos instalar Windows 10.

### <a name="set-iso-file-location"></a>Establecer la ubicación del archivo ISO

Puede descargar un archivo ISO para una versión de evaluación de la versión más reciente de Windows 10 Enterprise [aquí](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise).
- Cuando se le pida que seleccione una plataforma, elija **64 bits**.

Después de descargar este archivo, el nombre será extremadamente largo (por ejemplo: 17763.107.101029-1455. rs5_release_svc_refresh_CLIENTENTERPRISEEVAL_OEMRET_x64FRE_en-US. ISO).

1. Para que sea más fácil escribir y recordar, cambie el nombre del archivo a **win10-eval. ISO**.
2. Cree un directorio en el equipo denominado **c:\iso** y mueva el archivo **win10-eval. ISO** allí, por lo que la ruta de acceso al archivo es **c:\iso\win10-eval.ISO**.
3. Si desea usar un nombre y una ubicación diferentes para el archivo, debe modificar los comandos de Windows PowerShell siguientes para usar el nombre y el directorio personalizados.

### <a name="determine-network-adapter-name"></a>Determinar el nombre del adaptador de red

El cmdlet Get-NetAdaper se usa a continuación para buscar automáticamente el adaptador de red que es más probable que se use para conectarse a Internet. Para probar este comando primero, ejecute lo siguiente en un símbolo del sistema de Windows PowerShell con privilegios elevados:

```powershell
(Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
```

La salida de este comando debe ser el nombre de la interfaz de red que se usa para conectarse a Internet. Compruebe que este es el nombre de interfaz correcto. Si no es el nombre de interfaz correcto, deberá editar el primer comando siguiente para usar el nombre de la interfaz de red.

Por ejemplo, si el comando anterior muestra Ethernet pero quiere usar ethernet2, el primer comando que aparece a continuación sería New-VMSwitch-Name AutopilotExternal-AllowManagementOS $true-NetAdapterName **ethernet2**.

### <a name="use-windows-powershell-to-create-the-demo-vm"></a>Usar Windows PowerShell para crear la máquina virtual de demostración

Todos los datos de la máquina virtual se crearán en la ruta de acceso actual en el símbolo del sistema de PowerShell. Considere la posibilidad de navegar a una nueva carpeta antes de ejecutar los siguientes comandos.

> [!IMPORTANT]
> **Conmutador de máquina**virtual: un conmutador de máquina virtual es la forma en que Hyper-V conecta las máquinas virtuales a una red. <br><br>Si previamente ha habilitado Hyper-V y la interfaz de red conectada a Internet ya está enlazada a un conmutador de máquina virtual, se producirá un error en los siguientes comandos de PowerShell. En este caso, puede eliminar el conmutador de máquina virtual existente (para que los siguientes comandos puedan crear uno) o puede volver a usar este conmutador de máquina virtual omitiendo el primer comando que aparece a continuación y modificando el segundo comando para reemplazar el nombre del modificador **AutopilotExternal** por el nombre del conmutador o cambiando el nombre del conmutador existente por "AutopilotExternal".<br><br>Si nunca ha creado un conmutador de máquina virtual externo antes, simplemente ejecute los comandos siguientes.

```powershell
New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal
Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
Start-VM -VMName WindowsAutopilot
```

Después de escribir estos comandos, conéctese a la máquina virtual que acaba de crear y espere a que se le pida que presione una tecla y arranque desde el DVD.  Puede conectarse a la máquina virtual haciendo doble clic en ella en el administrador de Hyper-V.

Vea el resultado del ejemplo siguiente. En este ejemplo, la máquina virtual se crea en el directorio **c:\autopilot** y se usa el comando vmconnect.exe (que solo está disponible en Windows Server). Si instaló Hyper-V en Windows 10, use el administrador de Hyper-V para conectarse a la máquina virtual.

<pre style="overflow-y: visible">
PS C:\autopilot&gt; dir c:\iso


    Directory: C:\iso


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/12/2019   2:46 PM     4627343360 win10-eval.iso

PS C:\autopilot&gt; (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name
Ethernet
PS C:\autopilot&gt; New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name

Name              SwitchType NetAdapterInterfaceDescription
----              ---------- ------------------------------
AutopilotExternal External   Intel(R) Ethernet Connection (2) I218-LM

PS C:\autopilot&gt; New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal

Name             State CPUUsage(%) MemoryAssigned(M) Uptime   Status             Version
----             ----- ----------- ----------------- ------   ------             -------
WindowsAutopilot Off   0           0                 00:00:00 Operating normally 8.0

PS C:\autopilot&gt; Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
PS C:\autopilot&gt; Start-VM -VMName WindowsAutopilot
PS C:\autopilot&gt; vmconnect.exe localhost WindowsAutopilot
PS C:\autopilot&gt; dir

    Directory: C:\autopilot

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/12/2019   3:15 PM                VMData
d-----        3/12/2019   3:42 PM                VMs

PS C:\autopilot&gt;
</pre>

### <a name="install-windows-10"></a>Instalar Windows 10

Asegúrese de que la máquina virtual se ha arrancado desde la ISO de instalación, haga clic en **siguiente** , haga clic en **instalar ahora** y complete el proceso de instalación de Windows. Consulte los siguientes ejemplos:

   ![Instalación de Windows instalación de Windows instalación de Windows instalación de Windows programa de instalación de Windows ](images/winsetup1.png) ![ ](images/winsetup2.png) ![ ](images/winsetup3.png) ![ ](images/winsetup4.png) ![ ](images/winsetup5.png) ![](images/winsetup6.png)

Después de que la máquina virtual se reinicie, en el caso de OOBE, seleccione **configurar para uso personal** o unirse a un **dominio** y, a continuación, elija una cuenta sin conexión en la pantalla de **Inicio de sesión** .  Esto le ofrecerá la forma más rápida de obtener el escritorio. Por ejemplo:

   ![Instalación de Windows](images/winsetup7.png)

Una vez completada la instalación, inicie sesión y compruebe que se encuentra en el escritorio de Windows 10 y, después, cree su primer punto de control de Hyper-V. Los puntos de control se usan para restaurar la máquina virtual a un estado anterior. En este laboratorio se crearán varios puntos de control, que se pueden usar posteriormente para volver a realizar el proceso.

   ![Instalación de Windows](images/winsetup8.png)

Para crear el primer punto de control, abra un símbolo del sistema de Windows PowerShell con privilegios elevados en el equipo que ejecuta Hyper-V (no en la máquina virtual) y ejecute lo siguiente:

```powershell
Checkpoint-VM -Name WindowsAutopilot -SnapshotName "Finished Windows install"
```

Haga clic en la máquina virtual **WindowsAutopilot** en el administrador de Hyper-V y compruebe que la **instalación de Windows finalizada** aparece en el panel puntos de control.

## <a name="capture-the-hardware-id"></a>Capturar el ID. de hardware

> [!NOTE]
> Normalmente, el ID. de dispositivo lo captura el OEM cuando ejecutan la herramienta OA3 en cada dispositivo del generador.  A continuación, el OEM envía el HH de 4K creado por la herramienta OA3 a Microsoft enviándolo con un informe de compilación de equipos (CBR).  Para los fines de este laboratorio, está actuando como el OEM (captura de 4K HH), pero no va a usar la herramienta OA3 para capturar la versión completa de 4K HH por diversos motivos (tendrá que instalar la herramienta OA3, el dispositivo no pudo tener una versión de licencia por volumen de Windows, es un proceso más complicado que usar un script de PS, etc.).  En su lugar, simulará la ejecución de la herramienta OA3 ejecutando un script de PowerShell, que captura el dispositivo 4K HH como la herramienta OA3.

Siga estos pasos para ejecutar el script de PS:

1. Abra un símbolo del sistema de Windows PowerShell con privilegios elevados y ejecute los siguientes comandos. Estos comandos son los mismos independientemente de si usa una máquina virtual o un dispositivo físico:

    ```powershell
    md c:\HWID
    Set-Location c:\HWID
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
    Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
    ```

Cuando se le pida que instale el paquete NuGet, elija **sí**.

Vea el resultado del ejemplo siguiente.

<pre>
PS C:\> md c:\HWID

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/14/2019  11:33 AM                HWID

PS C:\> Set-Location c:\HWID
PS C:\HWID> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
PS C:\HWID> Install-Script -Name Get-WindowsAutopilotInfo -Force

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\user1\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and
import the NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
PS C:\HWID> $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
PS C:\HWID> Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
PS C:\HWID> dir

    Directory: C:\HWID

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/14/2019  11:33 AM           8184 AutopilotHWID.csv

PS C:\HWID>
</pre>

Compruebe que haya un archivo de **AutopilotHWID.csv** en el directorio **c:\HWID** que tenga unos 8 KB de tamaño.  Este archivo contiene el formato completo de 4K HH.

> [!NOTE]
> Aunque la extensión. csv puede estar asociada a Microsoft Excel, no puede ver el archivo correctamente si hace doble clic en él. Para analizar correctamente los delimitadores de coma y ver el archivo en Excel, debe usar los **datos**  >  **de la función Text/CSV** en Excel para importar las columnas de datos adecuadas. No es necesario ver el archivo en Excel a menos que tenga curiosidad. El formato de archivo se validará cuando se importe en AutoPilot. A continuación se muestra un ejemplo de los datos de este archivo.

![Número de serie y hash de hardware](images/hwid.png)

Tendrá que cargar estos datos en Intune para registrar el dispositivo para el piloto automático, por lo que debe transferirse al equipo que va a usar para tener acceso al Azure Portal.  Si usa un dispositivo físico en lugar de una máquina virtual, puede copiar el archivo en un stick USB.  Si usa una máquina virtual, puede hacer clic con el botón secundario en el archivo AutopilotHWID.csv y copiarlo; a continuación, haga clic con el botón derecho y pegue el archivo en el escritorio (fuera de la máquina virtual).

Si tiene problemas para copiar y pegar el archivo, solo tiene que ver el contenido en el Bloc de notas de la máquina virtual y copiar el texto en el Bloc de notas fuera de la máquina virtual. No use otro editor de texto para hacerlo.

> [!NOTE]
> Al copiar y pegar en máquinas virtuales o desde ellas, Evite hacer clic en otras cosas con el cursor del mouse entre el proceso de copiar y pegar, ya que esto puede vaciar o sobrescribir el portapapeles y requerir que se vuelva a iniciar. Ir directamente desde copiar para pegar.

## <a name="reset-the-vm-back-to-out-of-box-experience-oobe"></a>Restablecimiento de la máquina virtual a una versión rápida (OOBE)

Con el identificador de hardware capturado en un archivo, prepare la máquina virtual para la implementación de Windows AutoPilot restableciendo de nuevo en OOBE.

En la máquina virtual, vaya a **configuración > actualizar & Security > Recovery** y haga clic **en Introducción** en **restablecer este equipo**.
Seleccione **quitar todo** y **simplemente quitar mis archivos**. Por último, haga clic en **restablecer**.

![Restablecer el mensaje final de este equipo](images/autopilot-reset-prompt.jpg)

El restablecimiento de la VM o el dispositivo puede tardar unos minutos. Continúe con el paso siguiente (comprobar el nivel de suscripción) durante el proceso de restablecimiento.

![Restablecer la captura de pantalla de este equipo](images/autopilot-reset-progress.jpg)

## <a name="verify-subscription-level"></a>Comprobar el nivel de suscripción

Para este laboratorio, necesita una suscripción a AAD Premium.  Para saber si tiene una suscripción Premium, vaya a la hoja configuración de [inscripción de MDM](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility) . Observe el ejemplo siguiente:

**Azure Active Directory**  >  **Movilidad (MDM y MAM)**  >  **Microsoft Intune**

![MDM e Intune](images/mdm-intune2.png)

Si no aparece la hoja de configuración mostrada anteriormente, es probable que no tenga una suscripción **Premium** .  La inscripción automática es una característica que solo está disponible en AAD Premium.

Para convertir la cuenta de prueba de Intune en una cuenta gratuita de evaluación Premium, vaya a **Azure Active Directory**  >  **licencias**  >  **todos los productos**prueba  >  **/compra** y seleccione **evaluación gratuita** para Azure ad Premium o EMS E5.

![Restablecer el mensaje final de este equipo](images/aad-lic1.png)

## <a name="configure-company-branding"></a>Configuración de la personalización de marca de la compañía

Si ya tiene configurada la personalización de marca de empresa en Azure Active Directory, puede omitir este paso.

> [!IMPORTANT]
> Asegúrese de iniciar sesión con una cuenta de administrador global.

Vaya a [Personalización de marca de empresa en Azure Active Directory](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding), haga clic en **configurar** y configure cualquier tipo de personalización de marca de empresa que le gustaría ver durante el archivo Oobe.

![Configuración de la personalización de marca de la compañía](images/branding.png)

Cuando haya terminado, haga clic en **Guardar**.

> [!NOTE]
> Los cambios en la personalización de marca de empresa pueden tardar hasta 30 minutos en aplicarse.

## <a name="configure-microsoft-intune-auto-enrollment"></a>Configuración de la inscripción automática Microsoft Intune

Si ya tiene la inscripción automática de MDM configurada en Azure Active Directory, puede omitir este paso.

Abra [movilidad (MDM y MAM) en Azure Active Directory](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility) y seleccione **Microsoft Intune**. Si no ve Microsoft Intune, haga clic en **Agregar aplicación** y elija **Intune**.

Para los fines de esta demostración, seleccione **todos** en el **ámbito de usuario de MDM** y haga clic en **Guardar**.

![Ámbito de usuario de MDM en la hoja movilidad](images/autopilot-aad-mdm.png)

## <a name="register-your-vm"></a>Registrar la máquina virtual

La máquina virtual (o el dispositivo) se puede registrar a través de Intune o Microsoft Store para empresas (MSfB).  Ambos procesos se muestran aquí, pero <u>solo Seleccione uno</u> para los fines de este laboratorio. Se recomienda encarecidamente usar Intune en lugar de MSfB.

### <a name="autopilot-registration-using-intune"></a>Registro de AutoPilot mediante Intune

1. En Intune en el Azure portal, elija **inscripción de dispositivos**inscripción de  >  **Windows**  >  **dispositivos**de inscripción  >  **importar**.

    ![Importación de dispositivos de Intune](images/device-import.png)

    > [!NOTE]
    > Si elementos de menú como la **inscripción de Windows** no están activos, mire a la hoja de la derecha de la interfaz de usuario.  Es posible que tenga que proporcionar privilegios de configuración de Intune en una ventana de desafío que aparecía.

2. En **Agregar dispositivos Windows AutoPilot** en el extremo derecho, busque el archivo **AutopilotHWID.csv** que copió anteriormente en el equipo local.  El archivo debe contener el número de serie y el HH de 4K de la máquina virtual (o dispositivo).  Es correcto si otros campos (ID. de producto de Windows) se dejan en blanco.

    ![CSV DE HARDWARE](images/hwid-csv.png)

    Debe recibir una confirmación de que el archivo tiene el formato correcto antes de cargarlo, como se mostró anteriormente.

3. Haga clic en **importar** y espere hasta que se complete el proceso de importación. Esta operación puede tardar hasta 15 minutos.

4. Haga clic en **sincronizar** para sincronizar el dispositivo que acaba de registrar. Espere unos momentos antes de actualizar para comprobar que se ha agregado la máquina virtual o el dispositivo. Consulte el ejemplo siguiente.

   ![Importar ID. de hardware](images/import-vm.png)

### <a name="autopilot-registration-using-msfb"></a>Registro de AutoPilot mediante MSfB

> [!IMPORTANT]
> Si ya ha registrado la máquina virtual (o el dispositivo) mediante Intune, omita este paso.

Opcional: vea el vídeo siguiente para obtener información general sobre el proceso.

&nbsp;

> [!video https://www.youtube.com/embed/IpLIZU_j7Z0]

En primer lugar, necesita una cuenta de MSfB.  Puede usar la misma que creó anteriormente para Intune o seguir [estas instrucciones](https://docs.microsoft.com/microsoft-store/windows-store-for-business-overview) para crear una nueva.

A continuación, inicie sesión en [Microsoft Store para empresas](https://businessstore.microsoft.com/en-us/store) con su cuenta de prueba; para ello, haga clic en **iniciar sesión** en la esquina superior derecha de la Página principal.

Seleccione **administrar** en el menú superior y, a continuación, haga clic en el vínculo **programa de Windows AutoPilot Deployment** en la tarjeta **dispositivos** . Observe el ejemplo siguiente:

![Microsoft Store para Empresas](images/msfb.png)

Haga clic en el vínculo **Agregar dispositivos** para cargar el archivo CSV. Aparecerá un mensaje que indica que se está procesando la solicitud. Espere unos momentos antes de actualizar para ver que se ha agregado el nuevo dispositivo.

![Dispositivos](images/msfb-device.png)

## <a name="create-and-assign-a-windows-autopilot-deployment-profile"></a>Crear y asignar un perfil de implementación de Windows AutoPilot

> [!IMPORTANT]
> Los perfiles de AutoPilot pueden crearse y asignarse a la máquina virtual o al dispositivo registrados a través de Intune o MSfB.  Ambos procesos se muestran aquí, pero solo <U>Seleccione uno para los fines de este laboratorio</U>:

Elija una:
- [Creación de perfiles mediante Intune](#create-a-windows-autopilot-deployment-profile-using-intune)
- [Crear perfiles mediante MSfB](#create-a-windows-autopilot-deployment-profile-using-msfb)

### <a name="create-a-windows-autopilot-deployment-profile-using-intune"></a>Creación de un perfil de implementación de Windows AutoPilot mediante Intune

> [!NOTE]
> Aunque haya registrado el dispositivo en MSfB, seguirá apareciendo en Intune, aunque es posible que tenga que **sincronizar** y, a continuación, **Actualizar** la lista de dispositivos en primer lugar:

![Dispositivos](images/intune-devices.png)

> En el ejemplo anterior se enumeran un dispositivo físico y una máquina virtual. La lista solo debe incluir una de estas.

Para crear un perfil de Windows AutoPilot, seleccione **inscripción de dispositivos**inscripción de  >  **Windows**  >  **perfiles de implementación**

![Perfiles de implementación](images/deployment-profiles.png)

Haga clic en **crear perfil**.

![Crear Perfil de implementación](images/create-profile.png)

En la hoja **crear perfil** , use los valores siguientes:

| Parámetro | Value |
|---|---|
| Nombre | Perfil de laboratorio de AutoPilot |
| Descripción | en blanco |
| Convertir todos los dispositivos de destino en AutoPilot | No |
| Modo de implementación | Controlado por el usuario |
| Unirse a Azure AD como | Unido a Azure AD |

Haga clic en configuración rápida **(OOBE)** y configure las siguientes opciones:

| Parámetro | Value |
|---|---|
| EULA | Ocultar |
| Configuración de privacidad | Ocultar |
| Ocultar opciones de cuenta de cambio | Ocultar |
| Tipo de cuenta de usuario | Estándar |
| Aplicar plantilla de nombre de dispositivo | No |

Observe el ejemplo siguiente:

![Perfil de implementación](images/profile.png)

Haga clic en **Aceptar** y, a continuación, en **crear**.

> Si desea agregar una aplicación a su perfil a través de Intune, puede encontrar los pasos opcionales para hacerlo en el [Apéndice B: agregar aplicaciones a su perfil](#appendix-b-adding-apps-to-your-profile).

#### <a name="assign-the-profile"></a>Asignar el perfil

Los perfiles solo se pueden asignar a grupos, por lo que primero debe crear un grupo que contenga los dispositivos a los que se debe aplicar el perfil. En esta guía se proporcionarán instrucciones sencillas para asignar un perfil. para obtener instrucciones más detalladas, consulte [creación de un grupo de dispositivos AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group) y [asignación de un perfil de implementación de AutoPilot a un grupo de dispositivos](https://docs.microsoft.com/intune/enrollment-autopilot#assign-an-autopilot-deployment-profile-to-a-device-group), como lectura opcional.

Para crear un grupo, abra el Azure portal y seleccione **Azure Active Directory**  >  **grupos**  >  **todos los grupos**:

![Todos los grupos](images/all-groups.png)

Seleccione nuevo grupo en la hoja grupos para abrir la interfaz de usuario de grupos nuevos.  Seleccione el tipo de grupo "seguridad", asigne un nombre al grupo y seleccione el tipo de pertenencia "asignado":

Antes de hacer clic en **crear**, expanda el panel **miembros** , haga clic en el número de serie del dispositivo (aparecerá en **miembros seleccionados**) y, a continuación, haga clic en **seleccionar** para agregar el dispositivo a este grupo.

![Nuevo grupo](images/new-group.png)

Ahora haga clic en **crear** para terminar de crear el nuevo grupo.

Haga clic en **todos los grupos** y haga clic en **Actualizar** para comprobar que el nuevo grupo se ha creado correctamente.

Con un grupo creado que contenga el dispositivo, ahora puede volver y asignar su perfil a ese grupo. Vuelva a la página de Intune en el Azure Portal (una forma es escribir **Intune** en la barra de búsqueda superior del banner y seleccionar **Intune** en los resultados).

En Intune, seleccione **inscripción de dispositivos**inscripción de  >  **Windows**  >  **perfiles de implementación** para abrir la hoja de perfil.  Haga clic en el nombre del perfil que creó anteriormente (Perfil de laboratorio de AutoPilot) para abrir la hoja de detalles de ese perfil:

![Perfil de laboratorio](images/deployment-profiles2.png)

En **administrar**, haga clic en **asignaciones**y, después, con la pestaña **incluir** resaltada, expanda la hoja **seleccionar grupos** y haga clic en el **grupo de laboratorio de AP 1** (el grupo aparecerá en **miembros seleccionados**).

![Incluir grupo](images/include-group.png)

Haga clic en **Seleccionar** y después en **Guardar**.

![Incluir grupo](images/include-group2.png)

También es posible asignar usuarios específicos a un perfil, pero no trataremos este escenario en el laboratorio. Para obtener información más detallada, consulte [inscribir dispositivos Windows en Intune mediante Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="create-a-windows-autopilot-deployment-profile-using-msfb"></a>Crear un perfil de implementación de Windows AutoPilot mediante MSfB

Si ya ha creado y asignado un perfil mediante Intune mediante los pasos anteriores, omita esta sección.

Hay disponible un [vídeo](https://www.youtube.com/watch?v=IpLIZU_j7Z0) que cubre los pasos necesarios para crear y asignar perfiles en MSfB. Estos pasos también se resumen a continuación.

En primer lugar, inicie sesión en el [Microsoft Store para empresas](https://businessstore.microsoft.com/manage/dashboard) con la cuenta de Intune que creó inicialmente para este laboratorio.

Haga clic en **administrar** en el menú superior y, a continuación, haga clic en **dispositivos** en el árbol de navegación izquierdo.

![Administrar MSfB](images/msfb-manage.png)

Haga clic en el vínculo **programa de Windows AutoPilot Deployment** del icono **dispositivos** .

Para crear el perfil:

Seleccione el dispositivo en la lista de **dispositivos** :

![Crear MSfB](images/msfb-create1.png)

En el menú desplegable implementación de AutoPilot, seleccione **crear nuevo perfil**:

![Crear MSfB](images/msfb-create2.png)

Asigne un nombre al perfil, elija la configuración deseada y, a continuación, haga clic en **crear**:

![Crear MSfB](images/msfb-create3.png)

El nuevo perfil se agrega a la lista de implementación de AutoPilot.

Para asignar el perfil:

Para asignar o reasignar el perfil a un dispositivo, active las casillas situadas junto al dispositivo que registró para esta práctica y, a continuación, seleccione el perfil que desea asignar en el menú desplegable **implementación de AutoPilot** , como se muestra a continuación:

![MSfB asignar](images/msfb-assign1.png)

Confirme que el perfil se ha asignado correctamente al dispositivo deseado comprobando el contenido de la columna de **perfil** :

![MSfB asignar](images/msfb-assign2.png)

> [!IMPORTANT]
> El nuevo perfil solo se aplicará si el dispositivo no se ha iniciado y ha ido a través de OOBE. No se puede aplicar la configuración de un perfil diferente cuando se ha aplicado otro perfil. Es necesario volver a instalar Windows en el dispositivo para que el segundo perfil se aplique al dispositivo.

## <a name="see-windows-autopilot-in-action"></a>Consulte Windows AutoPilot en acción

Si apaga la máquina virtual después del último restablecimiento, es el momento de iniciarla de nuevo, por lo que puede progresar a través de la experiencia de OOBE de AutoPilot, pero no intenta volver a iniciar el dispositivo hasta que el **Estado del perfil** de su dispositivo en Intune haya cambiado de **no asignado** a **asignación** y finalmente **asignado**:

![Estado del dispositivo](images/device-status.png)

Además, asegúrese de esperar al menos 30 minutos desde el momento en que [configuró la personalización de marca](#configure-company-branding)de la empresa; de lo contrario, es posible que estos cambios no aparezcan.

> [!TIP]
> Si restablece el dispositivo previamente después de recopilar la información de 4K HH y, a continuación, le deja de volver a iniciarse en la primera pantalla de OOBE, es posible que tenga que reiniciar el dispositivo de nuevo para asegurarse de que el dispositivo se reconoce como un dispositivo AutoPilot y muestra la experiencia de OOBE de AutoPilot que espera.  Si no ve la experiencia de OOBE de AutoPilot, restablezca el dispositivo de nuevo (configuración > actualización & seguridad > recuperación y haga clic en introducción.  En restablecer este equipo, seleccione quitar todo y simplemente quitar mis archivos. Haga clic en restablecer).

- Asegúrese de que el dispositivo tiene una conexión a Internet.
- Encender el dispositivo
- Compruebe que aparecen las pantallas OOBE adecuadas (con la personalización de marca de empresa adecuada).  Debería ver la pantalla selección de región, la pantalla selección de teclado y la segunda pantalla de selección de teclado (que puede saltar).

![Página de inicio de sesión de OOBE](images/autopilot-oobe.jpg)

Poco después de llegar al escritorio, el dispositivo debería aparecer en Intune como un dispositivo AutoPilot **habilitado** .  Vaya al Azure Portal de Intune, seleccione **dispositivos > todos los dispositivos**y, a continuación, **actualice** los datos para comprobar que el dispositivo ha cambiado de deshabilitado a habilitado y el nombre del dispositivo está actualizado.

![Dispositivo habilitado](images/enabled-device.png)

Una vez que seleccione un idioma y una distribución del teclado, debe aparecer la pantalla de inicio de sesión con la marca de la empresa. Proporcione sus credenciales de Azure Active Directory y ya está listo.

Windows AutoPilot se usará para unir automáticamente el dispositivo a Azure Active Directory e inscribirlo en Microsoft Intune. Use los puntos de control que ha creado para volver a realizar este proceso con distintas configuraciones.

## <a name="remove-devices-from-autopilot"></a>Quitar dispositivos del AutoPilot

Para usar el dispositivo (o máquina virtual) para otros fines después de la finalización de este laboratorio, deberá quitar (anular su registro) del autopiloto a través de Intune o MSfB y, a continuación, restablecerlo.  Las instrucciones para cancelar el registro de dispositivos se pueden encontrar [aquí](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group) y [aquí](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal) y a continuación.

### <a name="delete-deregister-autopilot-device"></a>Eliminar (Desregistrar) dispositivo AutoPilot

Debe eliminar (o retirar o restablecer el restablecimiento de fábrica) el dispositivo de Intune antes de anular el registro del dispositivo de AutoPilot. Para eliminar el dispositivo de Intune (no Azure Active Directory), inicie sesión en el Azure Portal de Intune y vaya a **Intune > dispositivos > todos los dispositivos**.  Active la casilla situada junto al dispositivo que desea eliminar y, a continuación, haga clic en el botón eliminar en el menú superior.

![Eliminar un dispositivo](images/delete-device1.png)

Haga clic en **X** cuando tenga un desafío para completar la operación:

![Eliminar un dispositivo](images/delete-device2.png)

Esto eliminará el dispositivo de la administración de Intune y desaparecerá de **Intune > dispositivos > todos los dispositivos**. Pero esto todavía no anula el registro del dispositivo desde el piloto automático, por lo que el dispositivo todavía debería aparecer en **Intune > inscripción de dispositivos > la inscripción de windows > programa de implementación de Windows AutoPilot > dispositivos**.

![Eliminar un dispositivo](images/delete-device3.png)

La lista **dispositivos de > de Intune > todos los dispositivos** y la inscripción de dispositivos de **intune > > la inscripción de Windows > programa de implementación de Windows AutoPilot** enumeran la lista de dispositivos y son dos almacenes de archivos completamente independientes.  El primero (todos los dispositivos) es la lista de dispositivos inscritos actualmente en Intune.

> [!NOTE]
> Un dispositivo solo aparecerá en la lista todos los dispositivos una vez que se haya iniciado.  El último (programa de implementación de Windows AutoPilot > dispositivos) es la lista de dispositivos actualmente registrados en esa cuenta de Intune en el programa AutoPilot, que puede o no estar inscrito en Intune.

Para quitar el dispositivo del programa AutoPilot, seleccione el dispositivo y haga clic en eliminar.

![Eliminar un dispositivo](images/delete-device4.png)

Aparece un mensaje de advertencia que le recuerda que primero quite el dispositivo de Intune, que anteriormente lo hacía.

![Eliminar un dispositivo](images/delete-device5.png)

En este momento, se ha anulado la inscripción del dispositivo de Intune y también se ha anulado el registro de AutoPilot.  Después de unos minutos, haga clic en el botón **sincronizar** , seguido del botón **Actualizar** para confirmar que el dispositivo ya no aparece en el programa AutoPilot:

![Eliminar un dispositivo](images/delete-device6.png)

Una vez que el dispositivo ya no aparece, puede volver a usarlo para otros fines.

Si también quiere quitar el dispositivo de AAD, vaya a **Azure Active Directory > dispositivos > todos los dispositivos**, seleccione el dispositivo y haga clic en el botón Eliminar:

![Eliminar un dispositivo](images/delete-device7.png)

## <a name="appendix-a-verify-support-for-hyper-v"></a>Apéndice A: comprobar la compatibilidad de Hyper-V

A partir de Windows 8, el microprocesador del equipo host debe admitir la traducción de direcciones de segundo nivel (SLAT) para instalar Hyper-V. Consulte [Hyper-V: lista de CPU compatibles con slat para hosts](https://social.technet.microsoft.com/wiki/contents/articles/1401.hyper-v-list-of-slat-capable-cpus-for-hosts.aspx) para obtener más información.

Para comprobar que el equipo es compatible con SLAT, abra un símbolo del sistema de administrador, escriba **SystemInfo**, presione entrar, desplácese hacia abajo y revise la sección que aparece en la parte inferior de la salida, junto a requisitos de Hyper-V. Observe el ejemplo siguiente:

<pre style="overflow-y: visible">
C:>systeminfo

...
Hyper-V Requirements:      VM Monitor Mode Extensions: Yes
                           Virtualization Enabled In Firmware: Yes
                           Second Level Address Translation: Yes
                           Data Execution Prevention Available: Yes
</pre>

En este ejemplo, el equipo es compatible con SLAT e Hyper-V.

> Si uno o más requisitos se evalúan como **no** , el equipo no admite la instalación de Hyper-V.  Sin embargo, si solo la configuración de virtualización es incompatible, es posible que pueda habilitar la virtualización en el BIOS y cambiar la configuración de **Virtualización habilitada en firmware** de **no** a **sí**. La ubicación de esta configuración dependerá del fabricante y de la versión del BIOS, pero normalmente se encuentra asociado a la configuración de seguridad del BIOS.

También puede identificar la compatibilidad con Hyper-V mediante [las herramientas](https://blogs.msdn.microsoft.com/taylorb/2008/06/19/hyper-v-will-my-computer-run-hyper-v-detecting-intel-vt-and-amd-v/) proporcionadas por el fabricante del procesador, la herramienta [msinfo32](https://technet.microsoft.com/library/cc731397.aspx) , o puede descargar la utilidad [Coreinfo](https://technet.microsoft.com/sysinternals/cc835722) y ejecutarla, como se muestra en el ejemplo siguiente:

<pre style="overflow-y: visible">
C:>coreinfo -v

Coreinfo v3.31 - Dump information on system CPU and memory topology
Copyright (C) 2008-2014 Mark Russinovich
Sysinternals - www.sysinternals.com

Intel(R) Core(TM) i7-2600 CPU @ 3.40GHz
Intel64 Family 6 Model 42 Stepping 7, GenuineIntel
Microcode signature: 0000001B
HYPERVISOR      -       Hypervisor is present
VMX             *       Supports Intel hardware-assisted virtualization
EPT             *       Supports Intel extended page tables (SLAT)
</pre>

> [!NOTE]
> Se necesita un sistema operativo de 64 bits para ejecutar Hyper-V.

## <a name="appendix-b-adding-apps-to-your-profile"></a>Apéndice B: agregar aplicaciones a su perfil

### <a name="add-a-win32-app"></a>Agregar una aplicación Win32

#### <a name="prepare-the-app-for-intune"></a>Preparar la aplicación para Intune

Antes de poder extraer una aplicación en Intune para que forme parte de nuestro perfil de AP, es necesario "empaquetar" la aplicación para su entrega con la [herramienta de línea de comandosIntuneWinAppUtil.exe](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool).  Después de descargar la herramienta, recopile los tres bits de información siguientes para usar la herramienta:

1. La carpeta de origen de la aplicación
2. Nombre del archivo ejecutable de instalación.
3. La carpeta de salida del nuevo archivo

Para los fines de este laboratorio, usaremos la herramienta Notepad + + como nuestra aplicación de Win32.

Descargue el paquete de Notepad + + MSI [aquí](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available) y, a continuación, copie el archivo en una ubicación conocida, como C:\Notepad + + MSI.

Ejecute la herramienta IntuneWinAppUtil, proporcionando respuestas a las tres preguntas, por ejemplo:

![Agregar aplicación](images/app01.png)

Una vez finalizada la ejecución de la herramienta, debe tener un archivo. intunewin en la carpeta de salida, que ahora puede cargar en Intune mediante los pasos siguientes.

#### <a name="create-app-in-intune"></a>Creación de una aplicación en Intune

Inicie sesión en el Azure Portal y seleccione **Intune**.

Vaya a **Intune > aplicaciones de cliente > aplicaciones**y, luego, haga clic en el botón **Agregar** para crear un nuevo paquete de aplicación.

![Agregar aplicación](images/app02.png)

En **tipo de aplicación**, seleccione **aplicación de Windows (Win32)**:

![Agregar aplicación](images/app03.png)

En la hoja **archivo de paquete de aplicaciones** , busque el archivo **NPP. 7.6.3. Installer. x64. intunewin** en la carpeta de salida, ábralo y haga clic en **Aceptar**:

![Agregar aplicación](images/app04.png)

En la hoja configuración de la información de la **aplicación** , proporcione un nombre descriptivo, una descripción y un publicador, como:

![Agregar aplicación](images/app05.png)

En la hoja **configuración del programa** , proporcione los comandos de instalación y desinstalación:

Install: msiexec/i "npp.7.6.3.installer.x64.msi"/q Uninstall: msiexec/x "{F188A506-C3C6-4411-BE3A-DA5BF1EA6737}"/q

> [!NOTE]
> Lo más probable es que no tenga que escribir los comandos de instalación y desinstalación, ya que la [herramienta de línea de comandosIntuneWinAppUtil.exe](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool) los genera automáticamente cuando convirtió el archivo. msi en un archivo. intunewin.

![Agregar aplicación](images/app06.png)

Simplemente el uso de un comando de instalación como "Notepad + +. exe/S" no instalará el Bloc de notas + +. solo se iniciará la aplicación.  Para instalar realmente el programa, es necesario usar el archivo. msi en su lugar.  En realidad, el Bloc de notas + + no tiene una versión. msi de su programa, pero obtuvimos una versión. msi de un [proveedor de terceros](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available).

Haga clic en **Aceptar** para guardar la entrada y activar la hoja **requisitos** .

En la hoja **configuración de requisitos** , especifique la arquitectura del **sistema operativo** y la **versión mínima del sistema operativo**:

![Agregar aplicación](images/app07.png)

A continuación, configure las **reglas de detección**.  Para nuestros propósitos, seleccionaremos el formato manual:

![Agregar aplicación](images/app08.png)

Haga clic en **Agregar** para definir las propiedades de la regla.  En **tipo de regla**, seleccione **MSI**, que importará automáticamente el código de producto MSI correcto en la regla:

![Agregar aplicación](images/app09.png)

Haga clic en **Aceptar** dos veces para guardar, a medida que vuelve a la hoja principal **Agregar aplicación** para la configuración final.

**Códigos de retorno**: para nuestros propósitos, deje los códigos de retorno con sus valores predeterminados:

![Agregar aplicación](images/app10.png)

Haga clic en **Aceptar** para salir.

Puede omitir la configuración de la hoja de **ámbito final (etiquetas)** .

Haga clic en el botón **Agregar** para finalizar y guardar el paquete de la aplicación.

Una vez que el mensaje del indicador indica que se ha completado la adición.

![Agregar aplicación](images/app11.png)

Podrá encontrar la aplicación en la lista de aplicaciones:

![Agregar aplicación](images/app12.png)

#### <a name="assign-the-app-to-your-intune-profile"></a>Asignación de la aplicación a su perfil de Intune

> [!NOTE]
> Los siguientes pasos solo funcionan si ha [creado previamente un grupo en Intune y le ha asignado un perfil](#assign-the-profile).  Si no lo ha hecho, vuelva a la parte principal del laboratorio y complete estos pasos antes de volver aquí.

En el panel de **Intune > aplicaciones cliente > apps** , seleccione el paquete de la aplicación que ya ha creado para mostrar su hoja propiedades.  A continuación, haga clic en **asignaciones** en el menú:

![Agregar aplicación](images/app13.png)

Seleccione **Agregar grupo** para abrir el panel **Agregar grupo** que está relacionado con la aplicación.

Para nuestros propósitos, seleccione **requerido** en el menú desplegable **tipo de asignación** :

> **Disponible para los dispositivos inscritos** significa que los usuarios instalan la aplicación desde el portal de empresa aplicación o portal de empresa sitio Web.

Seleccione **grupos incluidos** y asigne los grupos creados previamente que usarán esta aplicación:

![Agregar aplicación](images/app14.png)

![Agregar aplicación](images/app15.png)

En el panel **seleccionar grupos** , haga clic en el botón **seleccionar** .

En el panel **asignar grupo** , seleccione **Aceptar**.

En el panel **Agregar grupo**, seleccione **Aceptar**.

En el panel **Asignaciones** de la aplicación, seleccione **Guardar**.

![Agregar aplicación](images/app16.png)

Ya ha completado los pasos para agregar una aplicación Win32 a Intune.

Para obtener más información sobre cómo agregar aplicaciones a Intune, vea [Intune independiente-administración de aplicaciones Win32](https://docs.microsoft.com/intune/apps-win32-app-management).

### <a name="add-office-365"></a>Agregar Office 365

#### <a name="create-app-in-intune"></a>Creación de una aplicación en Intune

Inicie sesión en el Azure Portal y seleccione **Intune**.

Vaya a **Intune > aplicaciones de cliente > aplicaciones**y, luego, haga clic en el botón **Agregar** para crear un nuevo paquete de aplicación.

![Agregar aplicación](images/app17.png)

En **tipo de aplicación**, seleccione **Office 365 Suite > Windows 10**:

![Agregar aplicación](images/app18.png)

En el panel **configurar App Suite** , seleccione las aplicaciones de Office que desea instalar.  Para los fines de este Labe, solo hemos seleccionado Excel:

![Agregar aplicación](images/app19.png)

Haga clic en **Aceptar**.

En el panel de **información del conjunto de aplicaciones** , escriba un nombre <i>único</i> para el conjunto y una descripción adecuada.

> escriba el nombre del conjunto tal como se muestra en el Portal de empresa. Asegúrese de que todos los nombres de conjuntos de aplicaciones que use sean únicos. Si el mismo nombre del conjunto ya existe, solo se muestra una de las aplicaciones a los usuarios en el portal de empresa.

![Agregar aplicación](images/app20.png)

Haga clic en **Aceptar**.

En el panel de **configuración del conjunto de aplicaciones** , seleccione **mensualmente** para el **canal de actualización** (cualquier selección sería correcta para los fines de este laboratorio).  Seleccione también **sí** para **Aceptar automáticamente el contrato de licencia para el usuario final de la aplicación**:

![Agregar aplicación](images/app21.png)

Haga clic en **Aceptar** y, a continuación, en **Agregar**.

#### <a name="assign-the-app-to-your-intune-profile"></a>Asignación de la aplicación a su perfil de Intune

> [!NOTE]
> Los siguientes pasos solo funcionan si ha [creado previamente un grupo en Intune y le ha asignado un perfil](#assign-the-profile).  Si no lo ha hecho, vuelva a la parte principal del laboratorio y complete estos pasos antes de volver aquí.

En el panel de **Intune > aplicaciones cliente > apps** , seleccione el paquete de Office que ya ha creado para mostrar su hoja propiedades.  A continuación, haga clic en **asignaciones** en el menú:

![Agregar aplicación](images/app22.png)

Seleccione **Agregar grupo** para abrir el panel **Agregar grupo** que está relacionado con la aplicación.

Para nuestros propósitos, seleccione **requerido** en el menú desplegable **tipo de asignación** :

> **Disponible para los dispositivos inscritos** significa que los usuarios instalan la aplicación desde el portal de empresa aplicación o portal de empresa sitio Web.

Seleccione **grupos incluidos** y asigne los grupos creados previamente que usarán esta aplicación:

![Agregar aplicación](images/app23.png)

![Agregar aplicación](images/app24.png)

En el panel **seleccionar grupos** , haga clic en el botón **seleccionar** .

En el panel **asignar grupo** , seleccione **Aceptar**.

En el panel **Agregar grupo**, seleccione **Aceptar**.

En el panel **Asignaciones** de la aplicación, seleccione **Guardar**.

![Agregar aplicación](images/app25.png)

En este punto, ha completado los pasos para agregar Office a Intune.

Para más información sobre cómo agregar aplicaciones de Office a Intune, consulte [asignación de aplicaciones de office 365 a dispositivos Windows 10 con Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).

Si instaló la aplicación Win32 (Notepad + +) y Office (solo Excel) según las instrucciones de este laboratorio, la máquina virtual las mostrará en la lista de aplicaciones, aunque puede tardar varios minutos en rellenarse:

![Agregar aplicación](images/app26.png)

## <a name="glossary"></a>Glosario

<table border="1">
<tr><td>OEM</td><td>Fabricante de equipo original</td></tr>
<tr><td>CSV</td><td>Valores separados por comas</td></tr>
<tr><td>MPC</td><td>Centro de partners de Microsoft</td></tr>
<tr><td>CSP</td><td>Proveedor de soluciones en la nube</td></tr>
<tr><td>MSfB</td><td>Microsoft Store para Empresas</td></tr>
<tr><td>AAD</td><td>Azure Active Directory</td></tr>
<tr><td>4K HH</td><td>Hash de hardware de 4K</td></tr>
<tr><td>CBR</td><td>Informe de compilación de equipos</td></tr>
<tr><td>EC</td><td>Comercio empresarial (servidor)</td></tr>
<tr><td>DDS</td><td>Servicio de directorio de dispositivos</td></tr>
<tr><td>OOBE</td><td>Experiencia rápida</td></tr>
<tr><td>máquina virtual</td><td>Máquina virtual</td></tr>
</table>
