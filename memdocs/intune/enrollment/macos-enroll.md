---
title: Configuración de la inscripción de dispositivos macOS
titleSuffix: Microsoft Intune
description: Descubra cómo configurar la inscripción de dispositivos macOS en Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c0973805a0646ec7df87f36eea183a9456f7e39
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865513"
---
# <a name="set-up-enrollment-for-macos-devices-in-intune"></a>Configuración de la inscripción de dispositivos macOS en Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune le permite administrar dispositivos macOS para proporcionar a los usuarios acceso a las aplicaciones y el correo electrónico de empresa.

Como administrador de Intune, puede configurar la inscripción para dispositivos macOS propiedad de la empresa y dispositivos macOS de propiedad personal ("Bring Your Own Device" o BYOD). 

## <a name="prerequisites"></a>Requisitos previos

Complete los siguientes requisitos previos antes de configurar la inscripción de dispositivos macOS:

- [Asegúrese de que el dispositivo es apto para la inscripción de dispositivos de Apple](https://support.apple.com/en-us/HT204142#eligibility).
- [Configurar dominios](../fundamentals/custom-domain-name-configure.md)
- [Establecer la entidad de MDM](../fundamentals/mdm-authority-set.md)
- [Crear grupos](../fundamentals/groups-add.md)
- [Configurar el Portal de empresa](../apps/company-portal-app.md)
- Asignación de licencias de usuario en el [Centro de administración de Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Obtener un certificado push MDM de Apple](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="user-owned-macos-devices-byod"></a>Dispositivos macOS propiedad del usuario (BYOD)

Puede permitir que los usuarios inscriban sus propios dispositivos personales en la administración de Intune. Esto se conoce como "bring your own device" o BYOD. Una vez completados los requisitos previos y asignadas las licencias a los usuarios, estos pueden inscribir sus dispositivos de estas maneras:
- visitando el [sitio web Portal de empresa](https://portal.manage.microsoft.com), o bien
- descargando la aplicación Portal de empresa de Mac en [aka.ms/EnrollMyMac](https://aka.ms/EnrollMyMac).

También puede enviar a los usuarios un vínculo sobre los pasos de inscripción en línea: [Inscriba el dispositivo macOS en Intune](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).

Para más información acerca de otras tareas de usuario final, consulte estos artículos:

- [Recursos sobre la experiencia del usuario final con Microsoft Intune](../fundamentals/end-user-educate.md)
- [Usar un dispositivo macOS con Intune](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>Dispositivos macOS propiedad de la empresa
Para las organizaciones que adquieran dispositivos para sus usuarios, Intune admite los métodos de inscripción de dispositivos macOS propiedad de la empresa siguientes:
- [Inscripción de dispositivo automatizada (ADE) de Apple](device-enrollment-program-enroll-macos.md): las organizaciones pueden adquirir dispositivos macOS a través de ADE. ADE permite implementar un perfil de inscripción "de forma inalámbrica" para incluir los dispositivos en la administración.
- [Administrador de inscripción de dispositivos (DEM)](device-enrollment-manager-enroll.md): puede usar una cuenta de DEM para inscribir hasta 1000 dispositivos.
- [Inscripción directa](device-enrollment-direct-enroll-macos.md): la inscripción directa no borra el dispositivo.

## <a name="block-macos-enrollment"></a>Bloqueo de la inscripción de macOS
De forma predeterminada, Intune permite la inscripción de dispositivos macOS. Para bloquear la inscripción de dispositivos macOS, vea [Set device type restrictions](enrollment-restrictions-set.md) (Establecer restricciones de tipos de dispositivo).

## <a name="enroll-virtual-macos-machines-for-testing"></a>Inscribir máquinas virtuales macOS para realizar pruebas

> [!NOTE]
> Las máquinas virtuales macOS solo se pueden usar para efectuar pruebas. No las use como dispositivos de producción para los usuarios finales. 

Las máquinas virtuales macOS se pueden inscribir con Parallels Desktop o con VMware Fusion para realizar pruebas en ellas. 

Si se usa Parallels Desktop, hay que indicar el tipo de hardware y el número de serie de las máquinas virtuales para que Intune pueda reconocerlas. Siga las instrucciones de Parallels para establecer el tipo de hardware y el [número de serie](http://kb.parallels.com/123455) con objeto de configurar los valores necesarios para las pruebas. Es recomendable que el tipo de hardware del dispositivo donde se ejecutan las máquinas virtuales y el tipo de hardware de las máquinas virtuales que vaya a crear sea el mismo. El tipo de hardware se encuentra en **menú Apple** > **Acerca de este Mac** > **Información del Sistema** > **Identificador del modelo**. 

En el caso de VMware Fusion, hay que [editar el archivo .vmx](https://kb.vmware.com/s/article/1014782) para establecer el modelo de hardware y el número de serie de la máquina virtual. Es recomendable que el tipo de hardware del dispositivo donde se ejecutan las máquinas virtuales y el tipo de hardware de las máquinas virtuales que vaya a crear sea el mismo. El tipo de hardware se encuentra en **menú Apple** > **Acerca de este Mac** > **Información del Sistema** > **Identificador del modelo**. 

## <a name="user-approved-enrollment"></a>Inscripción aprobada por el usuario

La inscripción de MDM aprobada por el usuario es un tipo de inscripción de macOS que se puede usar para administrar cierta configuración relacionada con la seguridad. Para más información, consulte la [documentación de soporte técnico de Apple](https://support.apple.com/HT208019).  
 
A partir de junio de 2020, todas las inscripciones de MDM de macOS nuevas en Intune, incluidas las que no se realizan a través de Inscripción de dispositivo automatizada (ADE), se consideran aprobadas por el usuario. El usuario final debe instalar manualmente el perfil de administración en **Preferencias del sistema** > **Perfiles** y, por tanto, proporcionar la aprobación del perfil de administración. Preferencias del sistema se inicia de forma automática desde la aplicación Portal de empresa para los usuarios BYOD de macOS. Las [instrucciones para instalar el perfil de administración](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp) se proporcionan en la aplicación Portal de empresa.     

Las inscripciones de MDM de BYOD macOS anteriores a junio de 2020 no pueden ser aprobadas por el usuario si el usuario final no ha proporcionado manualmente la aprobación del perfil de administración en **Preferencias del sistema** > **Perfiles**. En el caso de las inscripciones de BYOD posteriores a junio de 2020, la aplicación Portal de empresa inicia **Preferencias del sistema** para el usuario y el usuario tendrá que seleccionar Instalar. Si el usuario no ha aprobado el perfil de administración durante la inscripción, puede ir a **Preferencias del sistema** > **Perfiles**, elegir el perfil de administración y seleccionar **Aprobar** para aprobarlo más adelante.

### <a name="find-out-if-a-device-is-user-approved"></a>Determinación de si un dispositivo está aprobado por el usuario
1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Elija **Dispositivos** > **Todos los dispositivos** > elija el dispositivo > **Hardware**.
3. Compruebe el campo **Inscripción de usuario aprobada**.


## <a name="next-steps"></a>Pasos siguientes

Una vez que los dispositivos macOS se hayan inscrito, puede [crear una configuración personalizada para dispositivos macOS](../configuration/custom-settings-macos.md).
