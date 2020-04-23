---
title: Seguridad y privacidad de perfiles de VPN y Wi-Fi
titleSuffix: Configuration Manager
description: Conozca las recomendaciones de seguridad para administrar perfiles de Wi-Fi y VPN de dispositivos en Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705983"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Seguridad y privacidad para perfiles de Wi-Fi y VPN en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

## <a name="security-recommendations"></a>Recomendaciones de seguridad

Use los siguientes procedimientos recomendados de seguridad al administrar perfiles de Wi-Fi y VPN para dispositivos.

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>Elección de las opciones más seguras que los sistemas operativos cliente y la infraestructura de Wi-Fi y VPN admiten

Los perfiles de Wi-Fi y VPN constituyen un método muy práctico para administrar y distribuir de forma centralizada la configuración de Wi-Fi y VPN que sus dispositivos ya admiten. Configuration Manager no agrega ninguna funcionalidad de Wi-Fi o VPN. Identifique, implemente y siga las recomendaciones de seguridad indicadas para los dispositivos y la infraestructura.

## <a name="privacy-information"></a>Información de privacidad

Puede usar perfiles de Wi-Fi y VPN para configurar dispositivos cliente con el fin de conectarse a servidores VPN y Wi-Fi. A continuación, use Configuration Manager para evaluar si los dispositivos son compatibles después de aplicar los perfiles. El punto de administración envía información de compatibilidad al servidor de sitio. La información se almacena en la base de datos del sitio. La información se cifra cuando los dispositivos la envían al punto de administración, pero no se almacena en formato cifrado en la base de datos del sitio. La base de datos conserva la información hasta que la tarea de mantenimiento **Eliminar datos antiguos de administración de configuración** la elimina. El intervalo de eliminación predeterminado es de 90 días, pero puede cambiarlo. La información de compatibilidad no se envía a Microsoft.

De manera predeterminada, los dispositivos no evalúan perfiles de Wi-Fi y VPN. Además, debe configurar los perfiles y luego implementarlos en usuarios.  

Antes de configurar los perfiles de Wi-Fi o VPN, tenga en cuenta sus requisitos de privacidad.  
