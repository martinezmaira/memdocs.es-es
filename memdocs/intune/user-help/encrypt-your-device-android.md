---
title: Cifrado de un dispositivo Android en Intune | Microsoft Docs
description: Pasos para activar el cifrado de dispositivos Android cuando Intune lo requiera.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: d9e074def368927504c3f3c1761ec21b3ab62d22
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696276"
---
# <a name="encrypting-your-android-device"></a>Cifrado del dispositivo Android

El cifrado de dispositivos protege los archivos y las carpetas de accesos no autorizado si el dispositivo se pierde o se sustrae. Impide que las personas que no tienen código de acceso puedan acceder a los datos del dispositivo o leerlos. 

Para poder acceder a los recursos educativos o profesionales, es posible que su organización le requiera lo siguiente:

* [Cifrado del dispositivo](#encrypt-device)
* [Habilitación del arranque seguro](#enable-secure-startup)
* [Establecimiento de código de acceso de inicio, PIN u otro método de autenticación](#set-startup-passcode)  

> [!Note]
> Algunos dispositivos Android de Huawei, Vivo y OPPO no se pueden cifrar. Para obtener más información, consulte [Dispositivo cifrado, pero las aplicaciones dicen lo contrario](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

## <a name="encrypt-device"></a>Cifrado de dispositivos

Siga estos pasos para cifrar el dispositivo. El dispositivo puede reiniciarse varias veces. 

El nombre y la ubicación de la opción de cifrado variarán en función del fabricante del dispositivo y de la versión de Android. 

1. Abra la aplicación **Configuración**.
2. Escriba **seguridad** o **cifrar** en la barra de búsqueda de la aplicación para buscar la configuración relacionada.
3. Pulse la opción para cifrar el dispositivo. Siga las instrucciones en pantalla.  
4. Cuando se le solicite, establezca la contraseña de la pantalla de bloqueo, el PIN u otro método de autenticación (si la organización lo permite). 
5. Para comprobar de nuevo la configuración, abra la aplicación Portal de empresa o Microsoft Intune.
    * Usuarios se Portal de empresa: seleccione el dispositivo y pulse en **Comprobar configuración del dispositivo**. 
    * Usuarios de Microsoft Intune: tendrán que esperar hasta que se actualice la página, pero cuando lo haga, el estado de cifrado debe haber cambiado a compatible. 

## <a name="enable-secure-startup"></a>Habilitación del inicio seguro

Su organización puede requerir que habilite el inicio seguro como parte de su directiva de cifrado. Esta característica protege aún más el dispositivo al solicitar una contraseña o un PIN antes de que se inicie el teléfono. Es posible que tenga otras opciones de autenticación, pero variarán en función de lo que permita la organización. 

El nombre y la ubicación de la opción de inicio seguro variarán en función del fabricante del dispositivo y de la versión de Android. En algunos dispositivos, este ajuste se puede denominar **Protección segura**. 

1. Abra la aplicación **Configuración**.
2. Escriba **inicio seguro** en la barra de búsqueda de la aplicación.
3. Pulse **Inicio seguro** > **Require PIN when device turns on** (Requerir PIN cuando el dispositivo se active).
4. Cuando se le solicite, escriba el PIN del dispositivo.   
5. Para comprobar de nuevo la configuración, abra la aplicación Portal de empresa o Microsoft Intune.
    * Usuarios se Portal de empresa: seleccione el dispositivo y pulse en **Comprobar configuración del dispositivo**. 
    * Usuarios de Microsoft Intune: tendrán que esperar hasta que se actualice la página, pero cuando lo haga, el estado de cifrado debe haber cambiado a compatible.  


## <a name="set-startup-passcode"></a>Establecimiento del código de acceso de inicio   
Cuando [cifre el dispositivo](#encrypt-device) y [habilite el inicio seguro](#enable-secure-startup), se le pedirá que configure el PIN del dispositivo, la contraseña u otro método de autenticación (si lo permite la organización). No es necesario ningún paso más. 

Para elegir o cambiar el tipo de pantalla de bloqueo:

1. Abra la aplicación **Configuración**.
2. Escriba **bloqueo de pantalla** en la barra de búsqueda de la aplicación.
3. Pulse en la opción de **tipo de bloqueo de pantalla**.
4. Pulse en el tipo de bloqueo de pantalla que desea usar y siga las instrucciones en pantalla para confirmarlo.  

## <a name="troubleshoot"></a>Solución de problemas    
**Problema**: El botón de cifrado está deshabilitado.   

**Intente lo siguiente**: 
* Asegúrese de que el dispositivo está totalmente cargado y conectado. El cifrado puede tardar un rato y requiere una batería completa.   

**Problema**: Ve un mensaje en el que se indica que aún es necesario realizar el cifrado del dispositivo.  

**Pruebe lo siguiente**:
   *  [Establezca una pantalla de bloqueo](#set-startup-passcode) en el dispositivo. 
   * [Habilite el inicio seguro](#enable-secure-startup).

¿Aún necesita ayuda? Póngase en contacto con el equipo de soporte técnico de su empresa (visite el [sitio web del Portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980) para obtener la información de contacto), o escriba al <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">equipo de Microsoft Android</a>.  
