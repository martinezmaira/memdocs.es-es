---
title: ¿Qué ha ocurrido con la MDM híbrida?
titleSuffix: Configuration Manager
description: Obtenga información sobre el desuso de la administración híbrida de dispositivos móviles (MDM) en Configuration Manager
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d07a014cdcb3f371a90028ec09be3c0c939b8424
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724659"
---
# <a name="what-happened-to-hybrid-mdm"></a>¿Qué ha ocurrido con la MDM híbrida?

*Se aplica a: Configuration Manager (rama actual)*

> [!WARNING]
> Microsoft ha retirado la oferta de servicio de MDM híbrida a partir del 1 de septiembre de 2019. Los demás dispositivos MDM híbridos no recibirán directivas, aplicaciones ni actualizaciones de seguridad.

## <a name="remove-hybrid-mdm"></a>Quitar MDM híbrida

Si el sitio de Configuration Manager tenía una suscripción de Microsoft Intune, deberá quitarla.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Servicios de nube** y seleccione el nodo **Suscripción a Microsoft Intune**. Elimine la suscripción de Intune existente.

1. En el **Asistente para quitar suscripciones de Microsoft Intune**, seleccione la opción para **quitar Microsoft Intune suscripción de Configuration Manager**y, a continuación, haga clic en **siguiente**.

1. Complete el asistente.

## <a name="deprecation-announcement"></a>Anuncio de desuso

La siguiente nota es el anuncio de desuso original:

> [!NOTE]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). A partir de la versión de servicio 1902 de Intune, prevista para finales de febrero de 2019, los nuevos clientes no pueden crear una conexión híbrida.
> <!--Intune feature 2683117-->  
> Desde que lo lanzamos en Azure hace más de un año, Intune ha agregado cientos de nuevas funcionalidades solicitadas por el cliente y que se encuentran a la vanguardia del sector. Ahora ofrece muchas más funciones que las que hay disponibles a través de la administración híbrida de dispositivos móviles (MDM). Intune en Azure proporciona una experiencia administrativa más integrada y simplificada para sus necesidades de movilidad empresarial.
>
> Como resultado, la mayoría de los clientes eligen Intune en Azure en lugar de MDM híbrida. El número de clientes que usan MDM híbrida sigue disminuyendo a medida que más clientes se trasladan a la nube. Por lo tanto, el 1 de septiembre de 2019 Microsoft retirará la oferta de servicio de MDM híbrida.
>
> Este cambio no afecta a Configuration Manager local ni a la [administración conjunta para dispositivos con Windows 10](../../comanage/overview.md). Si no está seguro de si está usando la MDM híbrida, vaya al área de trabajo **Administración** de la consola de Configuration Manager, expanda **Cloud Services**y seleccione **Microsoft Intune suscripciones**. Si tiene una suscripción a Microsoft Intune configurada, el inquilino está configurado para MDM híbrida.
>
> **¿Cómo me afecta esto?**
>
> - Microsoft seguirá permitiendo el uso de MDM híbrida durante el próximo año. La característica continuará recibiendo importantes correcciones de errores. Microsoft brindará soporte a la funcionalidad existente en nuevas versiones de sistemas operativos, como la inscripción en iOS 12. No habrá ninguna característica nueva para MDM híbrida.  
>
> - Si migra a Intune en Azure antes del final de la oferta de MDM híbrida, el usuario final no debería notar nada.  
>
> - El 1 de septiembre de 2019, los dispositivos de MDM híbrida que queden ya no recibirán directivas, aplicaciones ni actualizaciones de seguridad.  
>
> - Las licencias siguen siendo las mismas. Las licencias de Intune en Azure se incluyen con MDM híbrida.  
>
> - La característica MDM local de Configuration Manager no está en desuso. A partir de Configuration Manager versión 1810, puede usar MDM local sin una conexión de Intune. Para obtener más información, consulte ya [no se necesita una conexión de Intune para las nuevas implementaciones de MDM local](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm).
>
> - La característica de acceso condicional local de Configuration Manager también está en desuso con MDM híbrida. Si usa el acceso condicional en dispositivos administrados con el cliente de Configuration Manager, asegúrese de que estén protegidos antes de migrar.
>     1. Configuración de directivas de acceso condicional en Azure
>     2. Configuración de directivas de cumplimiento en el portal de Intune
>     3. Finalizar la migración híbrida y establecer la entidad de MDM en Intune
>     4. Habilitación de la administración conjunta
>     5. Traslado de la carga de trabajo de administración conjunta de directivas de cumplimiento a Intune
>
>     Para más información, consulte [Acceso condicional con administración conjunta](../../comanage/quickstart-conditional-access.md).
>
> **¿Qué debo hacer para prepararme para este cambio?**
>
> - Comience a planear la migración de MDM desde la consola de Configuration Manager a Azure. Muchos clientes, incluidos los informáticos de Microsoft, han llevado a cabo este proceso. Para obtener más información, consulte este [caso práctico de Microsoft](https://aka.ms/Intune_MSFT).  
>
> - Póngase en contacto con su socio de registro o FastTrack para obtener ayuda. [FastTrack para Microsoft 365](https://aka.ms/hybrid_fasttrack) puede ayudar en la migración de MDM híbrida a Intune en Azure.
>
> Para obtener más información, consulte [la entrada de blog sobre soporte técnico de Intune](https://aka.ms/hybrid_notification).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre las características admitidas para administrar dispositivos MDM, consulte los siguientes artículos:

- [¿Qué es Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)
- [¿Qué es MDM local?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Administración de dispositivos con Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
