---
title: Creación de un perfil de certificado en Microsoft Intune - Azure | Microsoft Docs
description: Obtenga información sobre cómo usar certificados y perfiles de certificado de Protocolo de inscripción de certificados simple (SCEP) y Public Key Cryptography Standards (PKCS) con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22bfe44b95eedcdf87a41cfaaf959c72cfbe93e2
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423822"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>Uso de certificados para la autenticación en Microsoft Intune

Use certificados con Intune para autenticar a los usuarios en las aplicaciones y los recursos corporativos a través de VPN, Wi-Fi o perfiles de correo electrónico. Cuando se usan certificados para autenticar estas conexiones, los usuarios finales no tendrán que escribir nombres de usuario ni contraseñas, lo que puede facilitar su acceso. Los certificados también se usan para firmar y cifrar el correo electrónico mediante S/MIME.

## <a name="intune-supported-certificates-and-usage"></a>Certificados y uso admitidos por Intune

| Tipo              | Autenticación | Firma S/MIME | Cifrado S/MIME  |
|--|--|--|--|
| Certificado importado de Public Key Cryptography Standards (PKCS) |  | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible.](./media/certificates-configure/green-check.png)|
| PKCS#12 (o PFX)    | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible.](./media/certificates-configure/green-check.png) |  |
| Protocolo de inscripción de certificados simple (SCEP)  | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible.](./media/certificates-configure/green-check.png) | |

Para implementar estos certificados, debe crear y asignar perfiles de certificado a los dispositivos.

Cada perfil de certificado individual que cree es compatible con una sola plataforma. Por ejemplo, si usa certificados PKCS, creará un perfil de certificado PKCS para Android y otro independiente para iOS o iPadOS. Si también usa certificados SCEP para esas dos plataformas, tendrá que crear un perfil de certificado SCEP para Android y otro para iOS o iPadOS.

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>Consideraciones generales al usar una entidad de certificación de Microsoft

Cuando se usa una entidad de certificación (CA) de Microsoft:

- Para usar perfiles de certificado SCEP:
  - [configure un servidor de servicio de inscripción de dispositivos de red (NDES)](certificates-scep-configure.md#set-up-ndes) para usar con Intune.
  - [instale Microsoft Certificate Connector](certificates-scep-configure.md#install-the-microsoft-intune-connector).

- Para usar perfiles de certificado PKCS:
  - [instale el conector de certificados PFX para Microsoft Intune](certificates-imported-pfx-configure).
  
- Para usar certificados PKCS importados:
  - [Instale el conector de certificado PFX para Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).
  - Exporte los certificados de la entidad de certificación y, luego, impórtelos en Microsoft Intune. Consulte [el proyecto PFXImport de PowerShell](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

- Implemente certificados mediante los siguientes mecanismos:
  - [Perfiles de certificado de confianza](certificates-configure.md#create-trusted-certificate-profiles) para implementar en los dispositivos el certificado de CA raíz de confianza de la entidad de certificación raíz o intermedia (emisora).
  - Perfiles de certificados de SCEP
  - Perfiles de certificado PKCS
  - Perfiles de certificados PKCS importados

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>Consideraciones generales al usar una entidad de certificación de terceros

Cuando se usa una entidad de certificación (CA) de terceros (que no es de Microsoft):

- Para usar perfiles de certificado SCEP:
  - Configure la integración con una entidad de certificación de terceros de [uno de nuestros asociados admitidos](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners). La configuración incluye las siguientes instrucciones de la entidad de certificación de terceros para completar la integración de su CA con Intune.
  - [Cree una aplicación en Azure AD](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration) que delegue derechos en Intune para realizar la validación del desafío de certificado SCEP.

- Los certificados PKCS importados requieren que [instale el conector de certificado PFX para Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).

- Implemente certificados mediante los siguientes mecanismos:
  - [Perfiles de certificado de confianza](certificates-configure.md#create-trusted-certificate-profiles) para implementar en los dispositivos el certificado de CA raíz de confianza de la entidad de certificación raíz o intermedia (emisora).
  - Perfiles de certificados de SCEP
  - Perfiles de certificado PKCS *(solo se admite con la [plataforma de PKI de Digicert ](certificates-digicert-configure.md))*
  - Perfiles de certificados PKCS importados

## <a name="supported-platforms-and-certificate-profiles"></a>Plataformas compatibles y perfiles de certificado

| Plataforma              | Perfil de certificado de confianza | Perfil de certificado PKCS | Perfil de certificado SCEP | Perfil de certificado PKCS importado  |
|--|--|--|--|---|
| Administrador de dispositivos Android | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible.](./media/certificates-configure/green-check.png)|  ![Compatible](./media/certificates-configure/green-check.png) |
| Android Enterprise <br> - Totalmente administrado (propietario del dispositivo)   | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png)  | ![Compatible](./media/certificates-configure/green-check.png) |  ![Compatible](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> - Dedicado (propietario del dispositivo)   | ![Compatible](./media/certificates-configure/green-check.png)  | ![Compatible](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png)  | ![Compatible](./media/certificates-configure/green-check.png)|
| Android Enterprise <br> -Perfil de trabajo de propiedad corporativa   | ![Compatible](./media/certificates-configure/green-check.png)  | ![Compatible](./media/certificates-configure/green-check.png)  | ![Compatible](./media/certificates-configure/green-check.png)  | ![Compatible.](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> - Perfil de trabajo    | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png) | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png) |
| macOS                 | ![Compatible](./media/certificates-configure/green-check.png) |  ![Compatible](./media/certificates-configure/green-check.png) |![Compatible.](./media/certificates-configure/green-check.png)|![Compatible.](./media/certificates-configure/green-check.png)|
| Windows 8.1 y posterior |![Compatible.](./media/certificates-configure/green-check.png)  |  |![Compatible](./media/certificates-configure/green-check.png) |   |
| Windows 10 y versiones posteriores  | ![Compatible.](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png) | ![Compatible](./media/certificates-configure/green-check.png) | ![Compatible.](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>Exportación del certificado de entidad de certificación raíz de confianza

Para usar certificados PKCS, SCEP y PKCS importados, los dispositivos deben confiar en la entidad de certificación raíz. Para establecer la confianza, exporte el certificado de la entidad de certificación raíz de confianza y cualquier certificado de entidad de certificación intermedia o emisora, como un certificado público (.cer). Puede obtener estos certificados de la entidad de certificación emisora o desde cualquier dispositivo que confíe en ella.

Para exportar el certificado, consulte la documentación de la entidad de certificación. Tendrá que exportar el certificado público como un archivo .cer.  No exporte la clave privada, un archivo .pfx.

Usará este archivo .cer al [crear perfiles de certificado de confianza](#create-trusted-certificate-profiles) para implementar ese certificado en los dispositivos.

## <a name="create-trusted-certificate-profiles"></a>creación de perfiles de certificado de confianza

Cree e implemente un perfil de certificado de confianza antes de crear un perfil de certificado SCEP, PKCS o PKCS importado. La implementación de un perfil de certificado de confianza en los mismos grupos que reciben los otros tipos de perfiles de certificado garantiza que cada dispositivo pueda reconocer la legitimidad de la entidad de certificación. Esto incluye perfiles como los de VPN, Wi-Fi y correo electrónico.

Los perfiles de certificado SCEP hacen referencia directamente a un perfil de certificado de confianza. Los perfiles de certificado PKCS no hacen referencia directamente al perfil de certificado de confianza, pero sí al servidor que hospeda la entidad de certificación. Los perfiles de certificado PKCS importados no hacen referencia directamente al perfil de certificado de confianza, pero pueden usarlo en el dispositivo. La implementación de un perfil de certificado de confianza en los dispositivos garantiza que se establece esta confianza. Cuando un dispositivo no confía en la entidad de certificación raíz, se producirá un error en la directiva de perfil de certificado SCEP o PKCS.

Cree un perfil de certificado de confianza independiente para cada plataforma de dispositivo que quiera admitir, como lo haría con los perfiles de certificado SCEP, PKCS y PKCS importados.

> [!IMPORTANT]
> Los perfiles raíz de confianza que cree para la plataforma *Windows 10 y versiones posteriores* se muestran en el centro de administración de Microsoft Endpoint Manager como perfiles de la plataforma *Windows 8.1 y versiones posteriores*. 
>
> Se trata de un problema conocido con la presentación de la plataforma de los perfiles de certificado de confianza. Aunque el perfil muestra una plataforma de Windows 8.1 y versiones posteriores, es funcional para Windows 10 y versiones posteriores.

> [!NOTE]
> El perfil *Certificado de confianza* de Intune solo se puede usar para proporcionar certificados raíz o intermedios. El propósito de implementar estos certificados es establecer una cadena de confianza. Microsoft no admite el uso del perfil de certificado de confianza para ofrecer certificados que no sean raíz o intermedios. Es posible que se le impida importar certificados que no se consideren raíz o intermedios al seleccionar el perfil de certificado de confianza en el portal de Intune. Aunque pueda importar e implementar un certificado que no sea raíz o intermedio con este tipo de perfil, es probable que se produzcan resultados inesperados entre distintas plataformas, como iOS y Android.

### <a name="to-create-a-trusted-certificate-profile"></a>Para crear un perfil de certificado de confianza

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione y vaya a **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

   ![Navegación a Intune y creación de un perfil para un certificado de confianza](./media/certificates-configure/certificates-configure-profile-new.png)

3. Escriba las propiedades siguientes:
   - **Plataforma**: elija la plataforma de los dispositivos que recibirán este perfil.
   - **Perfil**: seleccione **Certificado de confianza**.
  
4. Seleccione **Crear**.

5. En **Básico**, escriba las propiedades siguientes:
   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil es *Perfil de certificado de confianza en toda la empresa*.
   - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.

7. En **Configuración**, especifique el archivo cer. del certificado de la entidad de certificación raíz de confianza que exportó anteriormente. 

   Solo para dispositivos Windows 8.1 y Windows 10, seleccione el **almacén de destino** del certificado de confianza. Las opciones son:

   - **Almacén de certificados de equipo - Raíz**
   - **Almacén de certificados de equipo - Intermedio**
   - **Almacén de certificados de usuario - Intermedio**

   ![Crear un perfil y cargar un certificado de confianza](./media/certificates-configure/certificates-configure-profile-fill.png)

8. Seleccione **Siguiente**.

9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

   Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione el usuario o los grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

    Seleccione **Siguiente**.

11. (*Se aplica solo a Windows 10*) En **Reglas de aplicación**, especifique las reglas de aplicación para restringir la asignación de este perfil. Puede elegir asignar o no asignar el perfil en función de la edición del sistema operativo o la versión de un dispositivo.

  Para más información, consulte [Reglas de aplicabilidad](../configuration/device-profile-create.md#applicability-rules) en *Creación de un perfil de dispositivo en Microsoft Intune*.

12. En **Revisar y crear**, revise la configuración. Si selecciona Crear, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

## <a name="additional-resources"></a>Recursos adicionales

- [Asignar perfiles de dispositivo](../configuration/device-profile-assign.md)  
- [Usar S/MIME para firmar y cifrar mensajes de correo electrónico](certificates-s-mime-encryption-sign.md)  
- [Uso de entidades de certificación de terceros](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>Pasos siguientes

Cree perfiles de certificado SCEP, PKCS o PKCS importados para cada plataforma que quiera usar. Para continuar, vea los artículos siguientes:

- [Configuración de la infraestructura para admitir certificados SCEP con Intune](certificates-scep-configure.md)  
- [Configuración y administración de certificados PKCS con Intune](certficates-pfx-configure.md)  
- [Creación de un perfil de certificado PKCS importado](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)

Más información sobre [conectores de certificados](certificate-connectors.md)