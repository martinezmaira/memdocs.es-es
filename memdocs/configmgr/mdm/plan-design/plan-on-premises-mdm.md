---
title: Planear la MDM local
titleSuffix: Configuration Manager
description: Planeación de la administración local de dispositivos móviles para administrar dispositivos móviles en Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724699"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Planear la MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Hay varias áreas clave que se deben revisar cuando se planea implementar la administración de dispositivos móviles (MDM) local en Configuration Manager:

- Dispositivos y versiones de sistema operativo compatibles
- Agregar los roles de sistema de sitio requeridos
- Comunicación segura
- Inscripción de dispositivos

> [!IMPORTANT]
> Aunque el sitio o cualquier dispositivo móvil no se conecta a Microsoft Intune, su organización todavía requiere licencias de Intune para usar esta característica. Para obtener más información, consulte [licencias de Microsoft Intune](https://docs.microsoft.com/intune/fundamentals/licenses).

Tenga en cuenta los siguientes requisitos antes de preparar la infraestructura de Configuration Manager para administrar la MDM local.

## <a name="supported-devices"></a><a name="bkmk_devices"></a> Dispositivos compatibles  

La rama actual de Configuration Manager admite la inscripción en la administración local de dispositivos móviles para dispositivos que ejecutan Windows 10. Estos tipos de dispositivos incluyen principalmente equipos portátiles, IoT y Surface Hub. Para obtener más información y la lista de ediciones específicas, consulte [versiones de sistema operativo compatibles con clientes y dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Roles de sistema de sitio

La MDM local requiere al menos uno de los siguientes roles de sistema de sitio:

- **Punto de proxy de inscripción** para admitir las solicitudes de inscripción.

- **Punto de inscripción** para admitir la inscripción de dispositivos.

- **Punto de administración de dispositivos** para la entrega de directivas. Este rol es una variación del punto de administración, pero permite la administración de dispositivos móviles.

- **Punto de distribución** para la entrega de contenido.

En función de las necesidades de su organización, puede instalar estos roles en el único servidor o por separado en servidores diferentes.

> [!NOTE]
> Debe configurar cada rol que se usa para MDM local como un punto de conexión HTTPS para comunicarse con dispositivos de confianza. Para obtener más información, vea [Comunicaciones de confianza requeridas](#bkmk_trustedComs).

Para obtener más información general, consulte [Plan for site System Servers and roles](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>Comunicaciones de confianza

MDM local requiere que se habiliten los roles de sistema de sitio para las comunicaciones HTTPS. En función de sus necesidades, puede usar la entidad de certificación (CA) de su organización para establecer las conexiones de confianza entre los servidores y los dispositivos. También puede usar una entidad de certificación disponible públicamente para que sea la autoridad de confianza. En cualquier caso, debe configurar los siguientes certificados:

- Un **certificado de servidor Web** en IIS en los servidores que hospedan los roles de sistema de sitio necesarios. Si un servidor hospeda varios roles de sistema de sitio, solo necesita un certificado para ese servidor. Si cada rol está en un servidor independiente, cada servidor necesita un certificado independiente.

- El **certificado raíz de confianza** de la CA que emite los certificados de servidor Web. Instale este certificado raíz en todos los dispositivos que necesiten conectarse a los roles de sistema de sitio.

Para obtener más información, consulte [configuración de certificados para comunicaciones de confianza en MDM local](../get-started/set-up-certificates-on-premises-mdm.md).

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>Inscripción de dispositivos

Para habilitar la inscripción de dispositivos para MDM local:

- Conceder permiso a los usuarios para inscribirse a través de la configuración de cliente

- Configurar dispositivos para comunicaciones de confianza con los servidores de sistema de sitio que hospedan los roles necesarios

Como alternativa a la inscripción iniciada por el usuario, puede configurar un paquete de inscripción masiva. Este paquete permite que el dispositivo se inscriba sin intervención del usuario. Entregue el paquete al dispositivo antes de que se aprovisione para su uso o después de que pase por su proceso de OOBE.

Para obtener más información, consulte Configuración de la [inscripción de dispositivos para MDM local](../get-started/set-up-device-enrollment-on-premises-mdm.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Instalar roles de sistema de sitio](../get-started/install-site-system-roles-for-on-premises-mdm.md)
