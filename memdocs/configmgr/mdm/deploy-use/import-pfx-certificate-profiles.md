---
title: Importar perfiles de certificado PFX
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo importar archivos PFX en Configuration Manager para generar certificados específicos del usuario que admitan el intercambio de datos cifrados.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef8c1656c12ead992d5305cdf86b1ab8fcfcb836
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608435"
---
# <a name="import-pfx-certificate-profiles"></a>Importar perfiles de certificado PFX

*Se aplica a: Configuration Manager (rama actual)*

Aprenda a crear un perfil de certificado mediante la importación de credenciales de certificados externos. En este artículo se resalta información específica acerca de los perfiles de certificado de intercambio de información personal (PFX). Para obtener más información sobre cómo crear y configurar estos perfiles, consulte [perfiles de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager admite diferentes tipos de almacenes de certificados para diferentes dispositivos y versiones de sistema operativo. Por ejemplo, Windows 10 y Windows 10 Mobile. Para obtener más información, consulte [requisitos previos](../../protect/plan-design/prerequisites-for-certificate-profiles.md)de los perfiles de certificado.

Use Configuration Manager para importar las credenciales de certificado y, a continuación, aprovisione los archivos PFX en los dispositivos. Puede usar estos archivos para generar certificados específicos del usuario para admitir el intercambio de datos cifrados.

> [!TIP]  
> Para obtener un tutorial paso a paso de este proceso, vea la entrada de blog [sobre cómo crear e implementar perfiles de certificado pfx en Configuration Manager](/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager).  

## <a name="create-a-profile"></a>Crear un perfil

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** , expanda **configuración de cumplimiento**, expanda **acceso a recursos**de la compañía y, a continuación, seleccione **perfiles de certificado**.

1. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear perfil de certificado**.

1. En la página **General** del **Asistente para crear Perfil de certificado**, especifique la información siguiente:  

    - **Nombre**: escriba un nombre único para el perfil de certificado. Puede utilizar un máximo de 256 caracteres.  

    - **Descripción**: proporcione una descripción general del perfil de certificado que le ayude a identificarlo en la consola de Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

1. Seleccione **intercambio de información personal: configuración de PKCS #12 (pfx): importar**. Esta opción importa información de un certificado existente para crear un perfil de certificado.

    > [!NOTE]
    > La opción **crear** solicita un certificado en nombre de un usuario de una entidad de certificación (CA) local conectada. Este proceso entrega el certificado a los clientes como archivos PFX de forma segura. Para obtener más información, consulte [creación de perfiles de certificado pfx mediante una entidad de certificación](create-pfx-certificate-profiles.md).

1. En la página **certificado pfx** del **Asistente para crear Perfil de certificado**, especifique el proveedor de almacenamiento de claves (KSP) del dispositivo:

    - **Instalar en Módulo de plataforma segura (TPM) si está presente**  
    - **Instalación en Módulo de plataforma segura (TPM); de lo contrario, error**
    - **Instalar en Windows Hello para empresas. de lo contrario, error**
    - **Instalar en proveedor de almacenamiento de claves de software**

1. En la página **plataformas admitidas** , elija las plataformas de dispositivos compatibles.

1. Complete el asistente.

## <a name="deploy-the-profile"></a>Implementar el perfil

Después de crear y aprovisionar un perfil de certificado, ahora está disponible en el nodo **perfiles de certificado** . Para obtener más información sobre cómo implementarla, consulte [implementación de perfiles de acceso de recursos](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="assign-primary-users"></a>Asignar usuarios primarios

Asigne los usuarios de destino como usuarios primarios en los dispositivos de Windows 10 en los que necesite instalar los certificados PFX. Para obtener más información, consulte [afinidad de dispositivo de usuario](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## <a name="provision-a-create-pfx-script"></a>Aprovisionamiento de un script de creación de PFX

Para importar un certificado PFX, use los siguientes cmdlets de PowerShell de Configuration Manager para aprovisionar un script de creación de PFX:

- [Get-CMClientCertificatePfx](/powershell/module/configurationmanager/get-cmclientcertificatepfx)
- [Import-CMClientCertificatePfx](/powershell/module/configurationmanager/import-cmclientcertificatepfx)
- [Remove-CMClientCertificatePfx](/powershell/module/configurationmanager/remove-cmclientcertificatepfx)

### <a name="example-script"></a>Script de ejemplo

Para aprovisionar un archivo PFX en un perfil de certificado para un usuario, abra PowerShell en un equipo con la consola de Configuration Manager. Cambie las variables con valores de su entorno.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>Consulte también

[Crear un nuevo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md)

[Creación de perfiles de certificado PFX mediante una entidad de certificación](create-pfx-certificate-profiles.md)

[Implementación de perfiles de Wi-Fi, VPN, correo electrónico y certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)