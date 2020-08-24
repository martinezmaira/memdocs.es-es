---
title: Dispositivos y clientes compatibles
titleSuffix: Configuration Manager
description: Obtenga información sobre qué versiones de SO admite Configuration Manager para clientes y dispositivos.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e573a2887bd527daac9a05fec2e83ef39fbfc4e1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700323"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Versiones de SO admitidas para clientes y dispositivos de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager admite la instalación de software cliente en equipos Windows y macOS.  

## <a name="general-requirements-and-limitations"></a>Limitaciones y requisitos generales

Revise las siguientes limitaciones y requisitos para todos los clientes:

- No se permite cambiar el tipo de inicio ni la configuración de **Iniciar sesión como** de ningún servicio de Configuration Manager. Este cambio puede impedir que servicios importantes funcionen correctamente.

## <a name="windows-computers"></a>Equipos Windows  

Para administrar las siguientes versiones del sistema operativo Windows, use el cliente que se incluye con Configuration Manager. Para obtener más información, consulte [Cómo implementar clientes en equipos Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).  

### <a name="supported-client-os-versions"></a>Versiones compatibles del sistema operativo de cliente

- **Windows 10**  

    Para obtener información más detallada, vea [Compatibilidad con Windows 10](support-for-windows-10.md).  

- **Windows 8.1** (x86, x64): Professional y Enterprise

#### <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

<!--3556025-->
[Windows Virtual Desktop](/azure/virtual-desktop/) es un servicio de virtualización de escritorio y aplicaciones que se ejecuta en Microsoft Azure. A partir de la versión 1906, use Configuration Manager para administrar estos dispositivos virtuales que ejecutan Windows en Azure.

Al igual que un servidor de terminal, algunos de estos dispositivos virtuales permiten varias sesiones de usuario activas simultáneas. Para facilitar el rendimiento del cliente, ahora en Configuration Manager se deshabilitan las directivas de usuario en todos los dispositivos que admiten estas sesiones de usuario múltiples. Aunque se habiliten directivas de usuario, el cliente las deshabilita de forma predeterminada en estos dispositivos, que incluyen sesiones múltiples de Windows 10 Enterprise y servidores de Terminal Server.

El cliente solo deshabilita la directiva de usuario cuando detecta este tipo de dispositivo durante una instalación nueva. Para un cliente existente de este tipo que actualice a esta versión, se conserva el comportamiento anterior. En un dispositivo existente, establece la configuración de directiva de usuario incluso si detecta que el dispositivo permite varias sesiones de usuario.

Si requiere una directiva de usuario en este escenario y acepta cualquier posible impacto en el rendimiento, use uno de los siguientes métodos para habilitar la directiva de usuario:

- En la versión 1910 y versiones posteriores, use la [configuración de cliente](../../clients/deploy/configure-client-settings.md). En el grupo **Directiva de cliente**, configure esta opción: **Habilitar directiva de usuario para varias sesiones de usuario**.<!-- 4737447 -->

- En la versión 1906, use el SDK de Configuration Manager con la [clase WMI de servidor SMS_PolicyAgentConfig](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md). Establezca la nueva propiedad `PolicyEnableUserPolicyOnTS` en `true`.

> [!Note]  
> No se puede usar la administración conjunta con un cliente que ejecuta varias sesiones de Windows 10 Enterprise. <!-- SCCMDocs-pr#3950 -->

A partir de la versión 2006, la plataforma de **sesión múltiple de Windows 10 Enterprise** está disponible en la lista de versiones de sistema operativo admitidas en objetos con reglas de requisitos o listas de aplicabilidad.<!--6527576-->

> [!NOTE]
> Si previamente ha seleccionado la plataforma de nivel superior **Windows 10**, esta acción ha seleccionado automáticamente todas las plataformas secundarias. Esta nueva plataforma no se selecciona automáticamente. Si desea agregar la **sesión múltiple de Windows 10 Enterprise**, selecciónela manualmente en la lista.

Para más información, consulte los siguientes artículos.

- [Compatibilidad con entornos de virtualización](support-for-virtualization-environments.md)
- [Administración de clientes de Configuration Manager en una infraestructura de escritorio virtual (VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)

### <a name="supported-server-os-versions"></a>Versiones compatibles del sistema operativo del servidor

- **Windows Server 2019**: Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>  
    (A partir de la versión 1806 de Configuration Manager)

- **Windows Server 2016**: Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: Workgroup, Standard  

- **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

Las siguientes versiones se refieren específicamente a la instalación Server Core del sistema operativo. <sup>[Nota 3](#bkmk_note3)</sup>  

Las versiones de canal semestrales de Windows Server son instalaciones Server Core, por ejemplo, Windows Server, versión 1809. Como un cliente de Configuration Manager, se admiten de la misma forma que la versión de canal semestral de Windows 10 asociada. Para más información, vea [Compatibilidad con Windows 10](support-for-windows-10.md).

- **Windows Server 2019** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a> Nota 1

Configuration Manager prueba y admite las ediciones de Windows Server Datacenter, pero está certificado oficialmente para Windows Server. No se ofrece soporte técnico de revisiones de Configuration Manager para problemas específicos de Windows Server Datacenter Edition. Para más información sobre el programa de certificación de Windows Server, vea [Windows Server Catalog](https://www.windowsservercatalog.com/).

#### <a name="note-2"></a><a name="bkmk_note2"></a> Nota 2

Para admitir la [instalación de inserción de cliente](../../clients/deploy/plan/client-installation-methods.md#client-push-installation), agregue el servicio del servidor de archivos del rol del servidor de Servicios de archivos y almacenamiento. Para más información sobre cómo instalar características de Windows en Server Core, vea [Install roles, role services, and features by using Windows PowerShell cmdlets](/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets) (Instalar roles, servicios de roles y características mediante los cmdlets de Windows PowerShell).  

#### <a name="note-3"></a><a name="bkmk_note3"></a> Nota 3

No se admite la nueva aplicación de Centro de Software en ninguna versión de Windows Server Core.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Equipos de Windows Embedded  

Administre dispositivos de Windows Embedded mediante la instalación del cliente de Configuration Manager en el dispositivo. Para obtener más información, vea [Planeación de la implementación del cliente en dispositivos Windows Embedded](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- Todas las características de cliente se admiten en sistemas de Windows Embedded que no tengan habilitados filtros de escritura.  

- Los clientes que usan uno de los siguientes filtros son compatibles con todas las características, excepto la administración de energía:  

  - Filtros de escritura mejorados (EWF)

  - Filtros de escritura basados en archivos RAM (FBWF)

  - Filtros de escritura unificados (UWF)  

- El catálogo de aplicaciones no es compatible con ningún dispositivo de Windows Embedded.  

### <a name="supported-os-versions"></a>Versiones de SO admitidas  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versión incluye el canal de servicio a largo plazo (LTSC). Para más información, vea [Información general de Windows 10 IoT Enterprise](/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Thin PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 con SP1** (x86, x64)

## <a name="windows-ce-computers"></a>Equipos de Windows CE

Administre dispositivos de Windows CE con el cliente heredado de dispositivos móviles de Configuration Manager que se incluye con Configuration Manager.  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- El cliente de dispositivo móvil necesita 0,78 MB de espacio de almacenamiento para la instalación. El inicio de sesión puede requerir hasta 256 KB de espacio adicional de almacenamiento.

- Las características de estos dispositivos móviles varían según el tipo de cliente y la plataforma. Para obtener información sobre qué funciones de administración son compatibles, vea [Elegir una solución de administración de dispositivos](../choose-a-device-management-solution.md).  

### <a name="supported-os-versions"></a>Versiones de SO admitidas

- Windows CE 7.0 (procesadores ARM y x86)  

    > [!IMPORTANT]
    > La versión 2006 de Configuration Manager anula la compatibilidad con Windows CE 7.0 como cliente. El anuncio del desuso se realizó con la [versión 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated).

#### <a name="supported-languages-include"></a>Los idiomas admitidos son

- Chino (simplificado y tradicional)

- Inglés (EE.UU.)

- Francés (Francia)

- Alemán

- Italiano

- Japonés  

- Coreano  

- Portugués (Brasil)  

- Ruso  

- Español (España)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> Actualizaciones de seguridad extendida y Configuration Manager

El programa de [actualizaciones de seguridad extendida (ESU) ](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) es una opción de último recurso para aquellos clientes que necesitan ejecutar determinados productos de Microsoft heredados más allá del final del soporte técnico. Por ejemplo, Windows 7. Incluye actualizaciones de seguridad críticas o importantes (tal y como se define en el [Centro de respuestas de seguridad de Microsoft [MSRC]](https://www.microsoft.com/msrc)) durante un máximo de tres años después del final de la fecha de soporte extendido del producto.

Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Esto incluye todos los productos que se incluyen en el programa ESU. Las actualizaciones de seguridad publicadas en el programa ESU se publicarán en Windows Server Update Services (WSUS). Estas actualizaciones se mostrarán en la consola de Configuration Manager. Mientras que los productos que se incluyen en el programa ESU ya no se admiten para su uso con Configuration Manager, se puede usar la [versión más reciente publicada de la rama actual de Configuration Manager](../../servers/manage/updates.md#version-details) para implementar e instalar actualizaciones de seguridad de Windows publicadas en el programa. También se puede usar la última versión de lanzamiento para implementar Windows 10 en dispositivos que ejecutan Windows 7.

Las características de administración de cliente no relacionadas con la administración de actualizaciones de software de Windows o la implementación de SO dejarán de estar probadas en los sistemas operativos que se incluyen en el programa ESU y no garantizamos que sigan funcionando. Se recomienda encarecidamente actualizar o migrar a una versión actual de los sistemas operativos lo antes posible para recibir compatibilidad con la administración de clientes.

## <a name="mac-computers"></a>Equipos Mac  

Administre equipos Apple Mac con el cliente de Configuration Manager para macOS.  

El paquete de instalación del cliente macOS no se suministra con los medios de Configuration Manager. Descárguelo en el Centro de descarga de Microsoft, [Microsoft Endpoint Configuration Manager: cliente macOS (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850).  

Para obtener más información, consulte [How to deploy clients to Macs](../../clients/deploy/deploy-clients-to-macs.md) (Implementación de clientes en equipos Mac).  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- No se permite instalar o ejecutar el cliente de Configuration Manager para macOS en equipos con una cuenta que no sea la cuenta raíz. Si lo hace, servicios importantes podrían dejar de funcionar correctamente.  

### <a name="supported-versions"></a>Versiones admitidas

- **macOS Catalina (10.15)** (requiere la versión 1910 o posterior del sitio de Configuration Manager y el cliente de Configuration Manager para macOS, versión 5.0.8742.1000 o posterior)

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

## <a name="linux-and-unix-servers"></a>Servidores Linux y UNIX  

> [!Important]  
> La versión 1902 de Configuration Manager anula la compatibilidad de Linux y UNIX como cliente. El anuncio del desuso se realizó con la [versión 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

Los paquetes de instalación del cliente Linux y UNIX no se suministran con los medios de Configuration Manager. Descargue los **clientes para sistemas operativos adicionales** en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). Además de los paquetes de instalación de cliente, la descarga de cliente incluye el script que administra la instalación del cliente en cada equipo.  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- Para consultar las dependencias de archivo del sistema operativo para el cliente Linux y UNIX, consulte [Requisitos previos para la implementación del cliente en servidores UNIX y Linux](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

- Para obtener información general de las funciones de administración compatibles con Linux o UNIX, vea [Implementar clientes en servidores UNIX y Linux](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

- En versiones compatibles de Linux y UNIX, la versión enumerada incluye todas las posteriores versiones secundarias. Por ejemplo, CentOS versión 6 incluye CentOS 6.3. De manera similar, la compatibilidad con un sistema operativo que usa Service Packs (como SUSE Linux Enterprise Server 11 SP1), incluye los Service Packs posteriores para esa versión del sistema operativo.  

- Para obtener información sobre los paquetes de instalación de cliente y el agente universal, consulte [Implementar clientes en servidores UNIX y Linux](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

### <a name="supported-versions"></a>Versiones admitidas

Las siguientes versiones se admiten mediante el archivo .tar indicado.  

#### <a name="aix"></a>AIX  

|Version|Archivo TAR|  
|-|-|  
|Versión 6.1 (Power)|ccm-Aix61ppc.&lt;compilación\>.tar|  
|Versión 7.1 (Power)|ccm-Aix71ppc.&lt;compilación\>.tar|  

#### <a name="centos"></a>CentOS  

|Version|Archivo TAR|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="debian"></a>Debian  

|Version|Archivo TAR|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 8 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 8 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|Version|Archivo TAR|  
|-|-|  
|Versión 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;compilación\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Version|Archivo TAR|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|Archivo TAR|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="solaris"></a>Solaris  

|Version|Archivo TAR|  
|-|-|  
|Versión 10 x86|ccm-Sol10x86.&lt;compilación\>.tar|  
|Versión 10 SPARC|ccm-Sol10sparc.&lt;compilación\>.tar|  
|Versión 11 x86|ccm-Sol11x86.&lt;compilación\>.tar|  
|Versión 11 SPARC|ccm-Sol11sparc.&lt;compilación\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|Archivo TAR|  
|-|-|  
|Versión 10 SP1 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 10 SP1 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 11 SP1 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 11 SP1 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 12 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Version|Archivo TAR|  
|-|-|  
|Versión 10.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 10.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 12.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 12.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 14.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 14.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 16.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 16.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a> MDM local

Configuration Manager tiene características integradas para administrar dispositivos móviles locales sin instalar el software cliente. Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="supported-operating-systems"></a>Sistemas operativos compatibles

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versión incluye el canal de servicio a largo plazo (LTSC). Para más información, vea [Información general de Windows 10 IoT Enterprise](/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 Team para Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!IMPORTANT]
    > La versión 2006 de Configuration Manager anula la compatibilidad con Windows 10 Mobile y Windows 10 Mobile Enterprise como cliente. El anuncio del desuso se realizó con la [versión 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated).

## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Conector de Exchange Server  

Configuration Manager admite la administración limitada de dispositivos que se conectan a Exchange Server sin instalar el cliente de Configuration Manager. Para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="supported-versions-of-exchange-server"></a>Versiones admitidas de Exchange Server

- **Exchange Online (Office 365)** : esta versión incluye Business Productivity Online Standard Suite.  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** o **Exchange Server 2010 SP2**