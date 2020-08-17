---
title: Activar Windows Defender | Microsoft Docs
description: Obtenga información sobre cómo activar Windows Defender para tener acceso a los recursos de la empresa.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a57010a5c8089b0ac979cf43c3706467d83faea2
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110705"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Activar Windows Defender para tener acceso a los recursos de la empresa

Las organizaciones quieren asegurarse de que los dispositivos que acceden a sus recursos estén protegidos, por lo que es posible que exijan el uso de [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx). Windows Defender es un software antivirus que se incluye en Windows y que facilita la protección del dispositivo frente a virus y otros programas de malware y amenazas. 

En este artículo se describe cómo actualizar la configuración del dispositivo para satisfacer los requisitos de antivirus de la organización y resolver problemas de acceso. 

## <a name="turn-on-windows-defender"></a>Activar Windows Defender
Complete los pasos siguientes para activar Windows Defender en el dispositivo. 

1. Seleccione el menú **Inicio**.
2. En la barra de búsqueda, escriba **directiva de grupo**. Después, seleccione **Editar directiva de grupo** en los resultados que se muestran. Se abrirá el Editor de directivas de grupo local.
4. Seleccione **Configuración del equipo** > **Plantillas administrativas** > **Componentes de Windows** > **Antivirus de Windows Defender**. 
5. Desplácese hasta la parte inferior de la lista y seleccione **Desactivar Antivirus de Windows Defender**.  
6. Seleccione **Deshabilitado** o **No configurado**. Podría parecer contradictorio seleccionar estas opciones, ya que los nombres sugieren que Windows Defender se desactiva. No se preocupe, estas opciones realmente garantizan que está activado. 
7. Seleccione **Aplicar** > **Aceptar**.  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>Activación de la protección en tiempo real y la que proporciona la nube

Complete los pasos siguientes para activar la protección en tiempo real y la que proporciona la nube. De manera conjunta, estas características de antivirus protegen contra el spyware y pueden proporcionar correcciones para problemas de malware a través de la nube. 

1. Seleccione el menú **Inicio**.
2. En la barra de búsqueda, escriba **Seguridad de Windows**. Seleccione el resultado coincidente. 
3. Seleccione **Protección contra virus y amenazas**.
4. En **Configuración de antivirus y protección contra amenazas**, seleccione **Administrar la configuración**.
5. Active los conmutadores de **Protección en tiempo real** y **Protección que proporciona la nube**. 

Si no ve estas opciones en la pantalla, es posible que estén ocultas. Complete los pasos siguientes para que sean visibles.  

1. Seleccione el menú **Inicio**.  
2. En la barra de búsqueda, escriba **directiva de grupo**. Después, seleccione **Editar directiva de grupo** en los resultados que se muestran. Se abrirá el Editor de directivas de grupo local.
3. Seleccione **Configuración del equipo** > **Plantillas administrativas** > **Componentes de Windows** > **Seguridad de Windows** > **Protección antivirus y contra amenazas**.
4. Seleccione **Ocultar el área de protección contra virus y amenazas**.
5. Seleccione **Deshabilitado** > **Aplicar** > **Aceptar**.  

## <a name="update-your-antivirus-definitions"></a>Actualizar las definiciones de antivirus
Complete los pasos siguientes para actualizar las definiciones de antivirus.  
1. Seleccione el menú **Inicio**.
2. En la barra de búsqueda, escriba **Seguridad de Windows**. Seleccione el resultado coincidente. 
3. Seleccione **Protección contra virus y amenazas**.
4. En **Actualizaciones de protección contra virus y amenazas**, seleccione **Buscar actualizaciones**. Si no ve esta opción en la pantalla, complete el primer conjunto de pasos de [Activación de la protección en tiempo real](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection). Después, intente volver a buscar las actualizaciones. 

## <a name="next-steps"></a>Pasos siguientes  

¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para obtener información de contacto, consulte el [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
