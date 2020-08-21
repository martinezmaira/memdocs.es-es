---
title: Preguntas más frecuentes sobre Microsoft Endpoint Configuration Manager
titleSuffix: Configuration Manager
description: Preguntas más frecuentes sobre Microsoft Endpoint Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0b59ffa73bb2c7524f2eed29326f238d856adef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699320"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Preguntas más frecuentes sobre Microsoft Endpoint Configuration Manager

*Se aplica a: Configuration Manager (rama actual, rama de Technical Preview)*

A partir de la versión 1910, Configuration Manager forma parte de Microsoft Endpoint Manager. En este artículo se da respuesta a las preguntas más frecuentes.

## <a name="summary"></a>Resumen

Comience viendo el siguiente vídeo de dos minutos de Brad Anderson, vicepresidente corporativo de Microsoft para Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>Preguntas más frecuentes

### <a name="what-is-microsoft-endpoint-manager"></a>¿Qué es Microsoft Endpoint Manager?

Microsoft Endpoint Manager es una solución integrada para administrar todos los dispositivos. Microsoft aúna Configuration Manager e Intune con licencias simplificadas. Siga aprovechando las inversiones existentes en Configuration Manager y aproveche las ventajas de la eficacia de la nube de Microsoft a su propio ritmo.

Las siguientes soluciones de administración de Microsoft forman parte ahora de la marca **Microsoft Endpoint Manager**:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Análisis de escritorio](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Otras características de la [consola de administración de dispositivos](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760).

Para más información, consulte las siguientes entradas de Brad Anderson, vicepresidente corporativo de Microsoft para Microsoft 365:

- [Entrada de blog de anuncio](https://aka.ms/cmannounce)
- [Documento sobre la visión](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>¿Qué cambia en Configuration Manager con Microsoft Endpoint Manager?

Aparte del cambio de nombre, el funcionamiento de Configuration Manager en la versión 1910 sigue siendo el mismo.

Lo más destacado es el cambio de los nombres de carpeta de los componentes comunes en el menú Inicio, como la [consola de Configuration Manager](../servers/manage/admin-console.md#bkmk_open) y el [Centro de software](software-center.md#bkmk_open).

### <a name="how-do-we-refer-to-the-product-now"></a>¿Cómo se denomina el producto ahora?

- Al referirse a la solución completa que engloba todos los componentes: **Microsoft Endpoint Manager**

- Al referirse al componente local:
  - Al hacerlo por primera vez, use el nombre de marca completo: **Microsoft Endpoint Configuration Manager**
  - Para un uso general: **Configuration Manager**
  - Para un uso con restricción de espacio: **ConfigMgr**, solo cuando el nombre de uso general no quepa

### <a name="are-there-any-licensing-changes"></a>¿Hay algún cambio de licencia?

Sí. Tal como se anunció en Microsoft Ignite 2019, si tiene una licencia de Configuration Manager, ahora también disfrutará de una licencia de Intune para [administrar conjuntamente](../../comanage/overview.md) los equipos Windows. Para más información, vea [Preguntas más frecuentes sobre productos y licencias](product-and-licensing-faq.md#bkmk_mem).

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>¿Por qué todavía veo "System Center Configuration Manager" en algunas partes?

Realizar cambios en todos los productos, servicios y materiales auxiliares (como la documentación) lleva su tiempo.

También hay algunos componentes fundamentales que pueden no cambiar nunca. El servicio de Windows principal en los servidores de sitio sigue siendo **SMS_Executive**. El repositorio de GitHub que sirve de apoyo a esta documentación seguirá siendo **SCCMDocs**.

## <a name="next-steps"></a>Pasos siguientes

Conozca las [Novedades de las versiones incrementales de Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md).