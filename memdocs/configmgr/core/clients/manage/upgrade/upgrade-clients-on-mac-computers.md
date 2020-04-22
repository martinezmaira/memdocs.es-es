---
title: Actualización de clientes de macOS
titleSuffix: Configuration Manager
description: Actualice el cliente de Configuration Manager en equipos Mac.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696263"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Procedimientos para actualizar clientes de Configuration Manager en equipos Mac

*Se aplica a: Configuration Manager (rama actual)*

Siga los pasos generales que se describen en este artículo para actualizar el cliente de equipos Mac mediante una aplicación de Configuration Manager. También puede descargar el archivo de instalación del cliente de Mac, copiarlo a una ubicación de red compartida o en una carpeta local en el equipo Mac y, después, indicar a los usuarios que ejecuten la instalación de forma manual.  

> [!NOTE]  
> Antes de realizar estos pasos, asegúrese de que el equipo Mac cumple los requisitos previos. Consulte [Sistemas operativos compatibles con equipos Mac](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="download-the-latest-mac-client"></a>Descarga del cliente de Mac más reciente

El cliente de Mac para Configuration Manager no se suministra en los medios de instalación de Configuration Manager. Descárguelo en el Centro de descarga de Microsoft, [Microsoft Endpoint Configuration Manager: cliente macOS (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850). Los archivos de instalación de cliente de Mac se incluyen en un archivo de Windows Installer denominado **ConfigmgrMacClient.msi**.  

## <a name="create-the-mac-client-installation-file"></a>Creación del archivo de instalación del cliente de Mac

Ejecute **ConfigmgrMacClient.msi** en un equipo que ejecute Windows. Este instalador desempaquetará el archivo de instalación del cliente de Mac, denominado **Macclient.dmg**. De forma predeterminada, puede encontrar este archivo en la carpeta siguiente: **C:\Archivos de programa\Microsoft\System Center Configuration Manager for Mac client**.  

## <a name="extract-the-client-installation-files"></a>extraer los archivos de instalación del cliente

Copie **Macclient.dmg** en un equipo Mac. Monte el archivo Macclient.dmg en macOS y, después, copie el contenido en una carpeta del equipo Mac.  

## <a name="create-a-cmmac-file"></a>Creación de un archivo .cmmac

1. Abra la carpeta **Tools** (Herramientas) de los archivos de instalación del cliente de Mac. Use la herramienta **CMAppUtil** para crear un archivo .cmmac a partir del paquete de instalación del cliente. Usará este archivo para crear la aplicación de Configuration Manager.  

2. Copie el nuevo archivo **CMClient.pkg.cmmac** en una ubicación que esté disponible para el equipo en el que se ejecuta la consola de Configuration Manager.  

    Para obtener más información, consulte [Procedimientos adicionales para crear e implementar aplicaciones para equipos Mac](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="create-and-deploy-the-app"></a>Creación e implementación de la aplicación

1. En la consola de Configuration Manager, [cree una aplicación](../../../../apps/get-started/creating-mac-computer-applications.md) a partir del archivo **CMClient.pkg.cmmac**.  

2. [Implemente esta aplicación](../../../../apps/deploy-use/deploy-applications.md) en los equipos Mac de la jerarquía.  

## <a name="install-the-updated-client"></a>Instalación del cliente actualizado

El cliente de Configuration Manager existente en los equipos Mac informará al usuario de que hay una actualización disponible para instalar. Cuando los usuarios instalan al cliente, deben reiniciar su equipo Mac.  

Una vez que se reinicie el equipo, el **Asistente para inscripción de equipos** se ejecuta de forma automática para solicitar un nuevo certificado de usuario.

Si no usa la inscripción de Configuration Manager, pero instala el certificado de cliente independientemente de Configuration Manager, vea [Configuración de clientes para usar un certificado existente](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configuración de clientes para usar un certificado existente

Use este procedimiento para evitar que se ejecute el Asistente para inscripción de equipos y para configurar el cliente actualizado a fin de que use un certificado de cliente existente.  

1. En la consola de Configuration Manager, [cree un elemento de configuración](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) del tipo **Mac OS X**.  

1. Agregue un valor de tipo **Script**a este elemento de configuración.  

1. Agregue el script siguiente a la configuración:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Agregue el elemento de configuración a una [línea base de configuración](../../../../compliance/deploy-use/create-configuration-baselines.md). Después, [implemente la línea base de configuración](../../../../compliance/deploy-use/deploy-configuration-baselines.md) en todos los equipos Mac que instalan un certificado de forma independiente a Configuration Manager.  
