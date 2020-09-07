---
title: Requisitos de contraseña para dispositivos inscritos en Intune | Microsoft Docs
description: En este artículo se describe cómo cumplir los requisitos de contraseña de la organización para poder acceder a la red.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: efb3c261-1f6c-4d39-bfa4-18661f8c59c7
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: b9bdada31e280c7fdc8a5d7a5a0a4a7ab7d36ae3
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057294"
---
# <a name="device-password-requirements"></a>Requisitos de contraseña de dispositivo  

Recibirá un mensaje de Portal de empresa si la contraseña del dispositivo no cumple los requisitos de seguridad de la organización. Se aplican requisitos de contraseña para protegerlo a usted y a los datos de la organización contra el acceso no autorizado. Mientras no cree una contraseña más segura, es posible que se le bloquee el acceso a la red de la organización.  

Portal de empresa envía un mensaje por cada requisito de contraseña, por lo que es posible que reciba más de un mensaje a la vez. Pulse cualquier mensaje para consultar los detalles (si se proporcionan).  

En este artículo se enumeran todos los mensajes relacionados con la contraseña que se podrían recibir y se proporcionan detalles adicionales sobre cada requisito, en función de la plataforma del sistema operativo.     

## <a name="change-password-passcode-pin"></a>Cambio de la contraseña, el código de acceso y el PIN  

Por lo general, para acceder a la configuración de contraseña, puede abrir la aplicación de configuración en el dispositivo y buscar la *pantalla de bloqueo* o la *configuración de seguridad*.  

En los artículos siguientes se describe cómo actualizar la contraseña del dispositivo, en función de la plataforma del sistema operativo. Para obtener las instrucciones más actualizadas de un dispositivo específico, consulte la documentación de ayuda del fabricante del dispositivo.  

- [Establecer la contraseña del dispositivo Windows 10](set-or-change-your-password-windows.md)  
- [Establecer el código de acceso del dispositivo iOS](set-or-change-your-passcode-ios.md)  
- [Establecer el PIN o contraseña del dispositivo Android](set-your-pin-or-password-android.md)  


> [!IMPORTANT]
> Si ha cambiado la contraseña para cumplir los requisitos, pero sigue recibiendo notificaciones, reinicie el dispositivo.  

Si tiene preguntas específicas sobre los requisitos de contraseña de la organización, póngase en contacto con el personal de soporte técnico de TI.  

## <a name="windows-10-password-requirements"></a>Requisitos de contraseña de Windows 10

| Mensaje | Solución |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| La contraseña es obligatoria. | Establezca una contraseña. La organización requiere que escriba una contraseña para desbloquear el dispositivo. |
| La contraseña es demasiado sencilla. |  Asegúrese de que la contraseña no contenga números repetidos o secuenciales, como 1234 o 1111. |
| La contraseña es demasiado corta.| Actualice o establezca una contraseña con más caracteres. La organización requiere que la contraseña tenga una longitud determinada. La elección variará, pero la longitud mínima es de 4 caracteres, mientras que la máxima es de 16. |
| La contraseña debe contener únicamente números. | Establezca una contraseña que contenga únicamente números.|
| La contraseña solo puede contener caracteres alfanuméricos. | Establezca una contraseña que contenga una combinación de números y letras.|
| La contraseña debe contener caracteres complejos. | Agregue caracteres complejos, por ejemplo, números, letras mayúsculas y símbolos como `$`, `%` y `#`. Su organización necesita una combinación de letras, números y caracteres no alfanuméricos para que a otros usuarios les resulte más difícil averiguar la contraseña.|  
| La contraseña ha expirado. | Establezca una nueva contraseña. La organización requiere que cambie la contraseña después de un número determinado de días. |
| La contraseña se ha usado recientemente. | Elija una contraseña que no haya usado antes. La organización requiere que transcurra un período de tiempo determinado antes de volver a usar una contraseña. |

## <a name="ios-passcode-requirements"></a>Requisitos de código de acceso de iOS

| Mensaje | Solución |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| El código de acceso es obligatorio.| Establezca un código de acceso. La organización requiere que escriba un código de acceso para desbloquear el dispositivo. |
| El código de acceso es demasiado sencillo. |  Asegúrese de que el código de acceso no contenga números repetidos o secuenciales, como 1234 o 1111. |
| El código de acceso es demasiado corto. | Actualice o establezca un código de acceso con más caracteres. La organización requiere que el código de acceso tenga una longitud determinada. La elección variará, pero la longitud mínima es de 4 caracteres, mientras que la máxima es de 14. Al cambiar el código de acceso, es posible que aparezca un mensaje de Apple que le indicará que escriba seis o más caracteres. Este mensaje es simplemente una recomendación del sistema Apple. Si la organización solo necesita un código de acceso de cuatro o cinco caracteres, no es necesario que escriba uno de seis.|  
| El código de acceso debe contener únicamente números. | Establezca un código de acceso que contenga únicamente números.|
| El código de acceso solo puede contener caracteres alfanuméricos.| Establezca un código de acceso que contenga una combinación de números y letras.|
| El código de acceso debe contener caracteres no alfanuméricos. | Agregue caracteres especiales como `&`, `!`, `$`, `%` y `#`. La organización requiere una combinación de letras, números y caracteres no alfanuméricos para que a otros usuarios les resulte más difícil averiguar el código de acceso.|
| El código de acceso ha expirado. | Establezca una nueva contraseña. La organización requiere que cambie la contraseña después de un número determinado de días. |
| El código de acceso se ha usado recientemente.| Elija un código de acceso que no haya usado antes. La organización requiere que transcurra un período de tiempo determinado antes de volver a usar un código de acceso. |
|Se requiere la autenticación Touch ID o Face ID. | Configure Touch ID o Face ID. La organización requiere que se autentique con uno de estos métodos antes de usar Autorrellenar para contraseñas o datos de tarjetas de crédito. | 

## <a name="macos-password-requirements"></a>Requisitos de contraseña de macOS
| Mensaje | Solución |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| La contraseña es obligatoria. | Establezca una contraseña. La organización requiere que escriba una contraseña para desbloquear el dispositivo. |
| La contraseña es demasiado sencilla.|  Asegúrese de que la contraseña no contenga números repetidos o secuenciales, como 1234 o 1111. |
| La contraseña es demasiado corta. | Actualice o establezca una contraseña con más caracteres. La organización requiere que la contraseña tenga una longitud determinada.|
| La contraseña debe contener únicamente números. | Establezca una contraseña que contenga únicamente números.|
| La contraseña solo puede contener caracteres alfanuméricos. | Establezca una contraseña que contenga una combinación de números y letras.|
| La contraseña debe contener caracteres no alfanuméricos. | Agregue caracteres especiales como `&`, `!`, `$`, `%` y `#`. Su organización necesita una combinación de letras, números y caracteres no alfanuméricos para que a otros usuarios les resulte más difícil averiguar la contraseña.|
| La contraseña ha expirado. | Establezca una nueva contraseña. La organización requiere que cambie la contraseña después de un número determinado de días. |
| La contraseña se ha usado recientemente. | Elija una contraseña que no haya usado antes. La organización requiere que transcurra un período de tiempo determinado antes de volver a usar una contraseña. |

## <a name="android-password-requirements"></a>Requisitos de contraseña de Android
| Mensaje | Solución |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| La contraseña es obligatoria. | Establezca una contraseña o PIN. La organización requiere que escriba una contraseña para desbloquear el dispositivo. |
| La contraseña es demasiado sencilla. |  Asegúrese de que la contraseña o PIN no contenga números repetidos o secuenciales, como 1234 o 1111. |
| La contraseña es demasiado corta. | Actualice o establezca una contraseña con más caracteres. La organización requiere que la contraseña tenga una longitud determinada.|
| La contraseña debe contener números. | Establezca una contraseña o PIN que contenga números.|
| La contraseña debe contener letras. | Establezca una contraseña que contenga letras del alfabeto.|
| La contraseña debe contener caracteres alfanuméricos. | Establezca una contraseña que contenga una combinación de números y letras.|
| La contraseña debe contener caracteres alfanuméricos y símbolos. | Establezca una contraseña que contenga una combinación de letras, números y caracteres especiales como `&`, `!`, `$`, `%` y `#`. |
| La contraseña debe usar la tecnología biométrica.| Configure el dispositivo para que use la autenticación biométrica, como el reconocimiento de huellas digitales o facial.
| La contraseña ha expirado. | Establezca una nueva contraseña. La organización requiere que cambie la contraseña después de un número determinado de días. |
| La contraseña se ha usado recientemente. | Elija una contraseña que no haya usado antes. La organización requiere que transcurra un período de tiempo determinado antes de volver a usar una contraseña. |

## <a name="next-steps"></a>Pasos siguientes
Si después de actualizar la contraseña sigue recibiendo mensajes relacionados con la contraseña, pruebe a reiniciar el dispositivo. 

¿Aún necesita ayuda? Póngase en contacto con el personal de soporte técnico de TI. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  


