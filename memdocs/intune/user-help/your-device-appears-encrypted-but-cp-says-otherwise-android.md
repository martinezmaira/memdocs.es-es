---
title: El dispositivo Android parece estar cifrado | Microsoft Docs
description: Resolución del estado de cifrado en Portal de empresa y la aplicación Microsoft Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4fd08ba190654db5678766e34e3340330dcf3ca8
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "79346097"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>Dispositivo cifrado, pero las aplicaciones dicen lo contrario

Si Portal de empresa o la aplicación Microsoft Intune indican que el dispositivo no está cifrado, pero se está seguro de que sí lo está, pruebe los pasos descritos en este artículo.  

## <a name="add-a-startup-pin"></a>Agregar un PIN de inicio

Ciertos dispositivos Android le exigen que cree un PIN de inicio para garantizar que el dispositivo sea seguro. La ubicación de esta configuración estará en la aplicación de **Configuración** del dispositivo. El nombre y la ubicación de la configuración pueden variar. Por ejemplo, en Samsung Galaxy S7, la configuración se conoce como **Inicio seguro**. Para habilitarla y crear un código de acceso, vaya a **Configuración** > **Bloquear pantalla y seguridad** > **Inicio seguro**.  

## <a name="encrypt-the-entire-device"></a>Cifrado de todo el dispositivo

Esta sección solo se aplica a la aplicación Portal de empresa. Algunos dispositivos le ofrecerán la opción de cifrar todo el dispositivo o simplemente el espacio usado. Elija la opción de cifrar todo el dispositivo. Si ha seleccionado cifrar solo el espacio usado, haga lo siguiente:

1. [Quite este dispositivo del Portal de empresa](unenroll-your-device-from-intune-android.md).
2. Descifre el espacio usado.  
3. Cifre todo el dispositivo.  
4. Vuelva a inscribir el dispositivo.  

## <a name="downgrade-your-version-of-android"></a>Cambiar a la versión anterior de Android

Esta sección solo se aplica a la aplicación Portal de empresa. Si el dispositivo ofrece la opción de cambiar a la versión Android 6.0 y versiones posteriores, hágalo. Si intenta cambiar el dispositivo a una versión anterior, existe riesgo de pérdida de datos. Si no, se recomienda que se ponga en contacto con el equipo de soporte técnico de su empresa para resolver este problema. Obtenga la información de contacto del equipo de soporte técnico de su empresa en el [sitio web del Portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="specific-manufacturer-issues"></a>Problemas específicos del fabricante

Algunos dispositivos Android de la versión 7.0 y posteriores cifran los datos de maneras incoherentes con determinados estándares de la plataforma Android. Estos métodos de cifrado ponen en peligro la información del dispositivo. Como consecuencia, no se admiten estos dispositivos.

Para obtener una lista no exhaustiva de los dispositivos Android compatibles, vea el artículo [Sistemas operativos y exploradores compatibles en Intune](https://docs.microsoft.com/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices). Si su dispositivo no aparece en la lista, consulte al fabricante del dispositivo o póngase en contacto con el personal de soporte técnico.

> [!Note]
> Microsoft trabaja junto con los fabricantes para abordar cualquier problema que se encuentre durante las pruebas o que los usuarios informen. Este artículo se actualiza cada vez que hay nueva información disponible.

## <a name="update-devices"></a>Actualización de los dispositivos

Si no ha actualizado el dispositivo a la versión más reciente de Android, vaya a la aplicación de **Configuración** del dispositivo y seleccione **Actualizar**.  

## <a name="next-steps"></a>Pasos siguientes

¿Aún necesita ayuda? Póngase en contacto con el equipo de soporte técnico de su empresa (visite el [sitio web del Portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980) para obtener la información de contacto), o escriba al <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">equipo de Microsoft Android</a>.  
