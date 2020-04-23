---
title: Perfiles de VPN
titleSuffix: Configuration Manager
description: Aprenda a usar perfiles de VPN en Configuration Manager para implementar la configuración de VPN en los usuarios de la organización.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706253"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Perfiles de VPN en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--1283610-->
Use perfiles de VPN en Configuration Manager para implementar la configuración de VPN en los usuarios de la organización. Mediante la implementación de esta configuración, se minimiza la intervención del usuario final necesaria para conectarse a los recursos de la red de la empresa.  

Por ejemplo, quiere configurar todos los dispositivos Windows 10 con las opciones de configuración necesarias para conectarse a un recurso compartido de archivos de la red interna. Cree un perfil de VPN con la configuración necesaria para conectarse a la red interna. Luego, implemente el perfil para todos los usuarios que tengan dispositivos Windows 10. Los usuarios ven la conexión VPN en la lista de redes disponibles y pueden conectarse sin apenas esfuerzo.

Cuando se crea un perfil de VPN, puede incluir una amplia gama de opciones de seguridad. Estas opciones incluyen certificados para la validación de servidor y la autenticación de cliente que se aprovisionan por medio de perfiles de certificado de Configuration Manager. Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).

> [!Note]
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="supported-platforms"></a>Plataformas compatibles

En la tabla siguiente se describen los perfiles de VPN que se pueden configurar para varias plataformas de dispositivo.

|Tipo de conexión|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Sí|No|Sí|Sí|
|**F5 Edge Client**|Sí|No|Sí|Sí|
|**Dell SonicWALL Mobile Connect**|Sí|No|Sí|Sí|
|**VPN móvil de punto de comprobación**|Sí|No|Sí|Sí|
|**Microsoft SSL (SSTP)**|Sí|Sí|Sí|No|
|**Microsoft Automatic**|Sí|Sí|Sí|No|
|**IKEv2**|Sí|Sí|Sí|No|
|**PPTP**|Sí|Sí|Sí|No|
|**L2TP**|Sí|Sí|Sí|No|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Creación de perfiles de VPN](create-vpn-profiles.md)

## <a name="see-also"></a>Vea también

- [Requisitos previos de los perfiles de VPN](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [Seguridad y privacidad de los perfiles de VPN](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
