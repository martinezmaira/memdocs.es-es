---
title: archivo include
description: Archivo de inclusión
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183062"
---
Estos avisos proporcionan información importante que puede ayudarle a prepararse para las características y los cambios futuros de Intune.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Fin del soporte técnico de Microsoft Intune para Windows 10 Mobile<!--3544938-->
El soporte técnico estándar de Microsoft para Windows 10 Mobile finalizó en diciembre de 2019. Como se ha mencionado en esta declaración de soporte técnico, los usuarios de Windows 10 Mobile dejarán de recibir de Microsoft nuevas actualizaciones de seguridad, revisiones no relacionadas con la seguridad, opciones gratuitas de soporte técnico asistido o actualizaciones de contenido técnico en línea. En función del soporte técnico general del sistema operativo Mobile, el 10 de agosto de 2020 Microsoft Intune finalizará el soporte técnico del Portal de empresa de la aplicación de Windows 10 Mobile y del sistema operativo Windows 10 Mobile.

#### <a name="how-does-this-affect-me"></a>¿Cómo me afecta esto?
Si tiene dispositivos Windows 10 Mobile implementados en su organización, desde ahora y el 10 de agosto de 2020 puede inscribir nuevos dispositivos, agregar o quitar directivas y aplicaciones o actualizar cualquier configuración de administración. Sin embargo, a partir del 10 de agosto, se detendrán las nuevas inscripciones y, finalmente, se eliminará la administración de Windows 10 Mobile de la interfaz de usuario de Intune. Los dispositivos ya no se registrarán en el servicio de Intune y se eliminarán los datos de directivas y dispositivos.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio?
Puede comprobar los informes de Intune para ver qué dispositivos o usuarios pueden verse afectados. Vaya a **Dispositivos** > **Todos los dispositivos** y filtre por sistema operativo. Puede agregar columnas adicionales para ayudar a identificar qué usuarios de su organización tienen dispositivos que ejecutan Windows 10 Mobile. Solicite a los usuarios finales que actualicen sus dispositivos o que dejen de usar los dispositivos para el acceso corporativo.


### <a name="end-of-support-for-legacy-pc-management"></a>Fin de la compatibilidad con la administración heredada de equipos

La administración heredada de equipos dejará de ser compatible el 15 de octubre de 2020. Actualice los dispositivos a Windows 10 y vuelva a inscribirlos como dispositivos de administración de dispositivos móviles (MDM) para administrarlos por Intune.

[Más información](https://go.microsoft.com/fwlink/?linkid=2107122).


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Reducción de la compatibilidad con el administrador de dispositivos Android<!--5857738-->
El administrador de dispositivos Android (que a veces se conoce como "administración de Android heredada" y publicada con Android 2.2) es una manera de administrar dispositivos Android. Sin embargo, ahora hay una funcionalidad de administración mejorada disponible con [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (publicada con Android 5.0). Con el fin de realizar la transición a la administración de dispositivos moderna, más completa y segura, Google va a reducir la compatibilidad con el administrador de dispositivos en las nuevas versiones de Android.

#### <a name="how-does-this-affect-me"></a>¿Cómo me afecta esto?
Debido a estos cambios de Google, los usuarios de Intune se verán afectados de las siguientes maneras:  
- Intune solo podrá proporcionar compatibilidad completa con dispositivos Android administrados por el administrador de dispositivos que ejecuten Android 10 y versiones posteriores hasta el segundo trimestre de 2020. Los dispositivos administrados por el administrador de dispositivos que ejecuten Android 10 o versiones posteriores después de este periodo ya no se podrán administrar por completo. En concreto, los dispositivos afectados no recibirán nuevos requisitos de contraseña.
    - Los dispositivos Samsung Knox no se verán afectados en este período de tiempo porque el soporte extendido se proporciona a través de la integración de Intune con la plataforma Knox. Esto le proporciona más tiempo para planear la transición desde la administración del administrador de dispositivos.    
- Los dispositivos Android administrados por el administrador de dispositivos que permanezcan en versiones de Android inferiores a Android 10 no se verán afectados y se podrán seguir administrando por completo con el administrador de dispositivos.    
- En todos los dispositivos Android 10 y versiones posteriores, Google ha restringido a los agentes de administración del administrador de dispositivos, como el Portal de empresa, el acceso a la información de identificación del dispositivo. Esta restricción afecta a las siguientes características de Intune después de que un dispositivo se actualice a Android 10 o una versión posterior:  
    - El control de acceso a la red de VPN dejará de funcionar.   
    - La identificación de los dispositivos como propiedad de la empresa con el número IMEI o el número de serie no marcará automáticamente los dispositivos como propiedad de la empresa.  
    - El número IMEI y el número de serie ya no serán visibles para los administradores de TI en Intune. 
        > [!NOTE]
        > Esta situación solo afecta a los dispositivos administrados por el administrador de dispositivos en Android 10 y versiones posteriores; no a los administrados con Android Enterprise. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio?
Para evitar la reducción de la funcionalidad que tendrá lugar en el tercer trimestre de 2020, siga estas recomendaciones:
- No incorpore nuevos dispositivos a la administración del administrador de dispositivos.
- Si está previsto que un dispositivo reciba una actualización de Android 10, mígrelo de la administración del administrador de dispositivos a la administración de Android Enterprise o a las directivas de protección de aplicaciones.

#### <a name="additional-information"></a>Información adicional
- [Guía de Google para la migración desde el administrador de dispositivos a Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Documentación de Google sobre el plan para dejar de usar la API del administrador de dispositivos](https://developers.google.com/android/work/device-admin-deprecation)