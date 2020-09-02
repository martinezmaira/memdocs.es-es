---
title: Almacenamiento de una clave de recuperación en Intune mediante el sitio web del Portal de empresa
description: Cargue y almacene la clave de recuperación del dispositivo en el sitio web del Portal de empresa.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f0a674753ff23fca509bd21e6b52101104a6803f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910798"
---
# <a name="store-your-personal-filevault-key"></a>Almacenamiento de la clave de FileVault personal 

Almacene una clave de FileVault para el dispositivo macOS con cifrado personal. Además de satisfacer los requisitos de cifrado, el almacenamiento de la clave en Intune permite: 

* Recuperar o rotar la clave con facilidad y rapidez desde cualquier dispositivo. 
* Pedir ayuda al personal de soporte técnico en caso de tener que recuperar o rotar la clave, si no hay posibilidad de acceder a las aplicaciones o al sitio web para hacerlo usted mismo.


## <a name="retrieve-or-rotate-the-key"></a>Recuperación o rotación de la clave

Si se bloquea el dispositivo, puede recuperar la clave desde las siguientes ubicaciones:
   
- sitio web del Portal de empresa
- Aplicación Portal de empresa para iOS/iPadOS 
- Aplicación Portal de empresa para Android
- Aplicación de Intune
 
 El personal de soporte técnico de TI con acceso de administrador a Intune puede rotar automáticamente su clave de recuperación personal si el dispositivo se bloquea. También puede ver las claves, pero solo las que pertenezcan a dispositivos de propiedad corporativa. Los usuarios de soporte técnico de TI no pueden ver las claves de recuperación que pertenezcan a dispositivos personales.   


## <a name="do-i-need-to-store-my-key"></a>¿Tengo que almacenar la clave?  
Un usuario de soporte técnico de TI le informará si tiene que cargar una clave de recuperación personal. Si el departamento de TI de su organización normalmente se comunica con usted a través de notificaciones, es posible que reciba una notificación de las aplicaciones del Portal de empresa para iOS/iPadOS o Android. 

Solo se recomienda cargar una clave de recuperación si se encuentra en una de las siguientes situaciones:
* Ha cifrado el dispositivo antes de inscribirlo en la organización. 
* Ha cifrado el dispositivo manualmente mediante las preferencias del sistema de macOS.   

En función de las directivas de la organización, es posible que el acceso a los recursos corporativos se bloquee en el dispositivo hasta que se cargue la clave.  

## <a name="upload-personal-recovery-key"></a>Carga de la clave de recuperación personal 
Siga estos pasos para guardar la clave de FileVault personal del dispositivo Mac cifrado.  


1. Vaya al [sitio web del Portal de empresa](https://portal.manage.microsoft.com) e inicie sesión con su cuenta profesional o educativa. 
2. Seleccione el dispositivo cifrado.
3. Selecciona la opción pertinente para **almacenar la clave de recuperación**.  
4. Escriba la clave alfanumérica de 24 caracteres de FileVault.  
5. Vuelva a escribir la clave. Luego haga clic en **Guardar**.
6. El Portal de empresa intentará comprobar, rotar y guardar la clave de recuperación personal. No hay que realizar ninguna otra acción una vez que se ha guardado la clave. Si deja el sitio web antes de que se complete la carga, podrá ver su estado en la página de detalles del dispositivo la próxima vez que inicie sesión.  

Para obtener más información sobre los mensajes que pueden aparecer durante este proceso, consulte [Mensajes del Portal de empresa](store-recovery-key.md#company-portal-messages).  

## <a name="company-portal-messages"></a>Mensajes del Portal de empresa

|Mensaje  |Significado  |
|---------|---------|
|Las claves deben coincidir. Compruébelas y vuelva a intentarlo.     | Aparece en el cuadro **Confirmar clave de recuperación** para informarle de que las claves no coinciden. Vuelva a escribir las claves en ambos campos e intente guardarlas de nuevo.        |
|No se pudo actualizar la clave de recuperación para el dispositivo.| Aparece como notificación del sistema en la parte superior de la pantalla para indicar que el Portal de empresa no pudo almacenar automáticamente una clave de recuperación. Para obtener más información, seleccione el dispositivo cifrado. Lea el mensaje de la parte superior de la página para conocer los pasos siguientes. |
|No se pudo cargar la clave de recuperación. Compruebe haya escrito la clave correcta y vuelva a intentarlo. Si el problema continúa, intente rotar la clave manualmente. Pulse para obtener más información.     | Aparece en la página de detalles del dispositivo y podría significar un par de cosas: En primer lugar, el Portal de empresa no pudo rotar y guardar la clave porque la clave especificada no es correcta. Compruebe que tiene la clave correcta y vuelva a intentarlo. La segunda posibilidad es que el dispositivo no se haya sincronizado con su organización en un tiempo. Para sincronizar las actualizaciones más recientes de su organización, seleccione el dispositivo y, luego, **Estado** > **Comprobar acceso**. Después, intente almacenar de nuevo la clave de recuperación. Por último, si el problema persiste, es posible que indique que la organización no ha habilitado FileVault por su parte. Póngase en contacto con el personal de soporte técnico de TI e indíquele que ha sincronizado el dispositivo, pero todavía no puede almacenar la clave de FileVault.         |
|La clave de recuperación se ha actualizado. Si alguna vez se bloquea el dispositivo y necesita recuperar la clave, inicie sesión en el Portal de empresa y seleccione **Obtener clave de recuperación**.    | Aparece en la página de detalles del dispositivo. La clave que guardó se rotó correctamente y la nueva clave de recuperación personal está almacenada.    |



## <a name="it-pro-support"></a>Soporte para profesionales de TI

Si forma parte del personal soporte técnico de TI, y quiere configurar y administrar el cifrado de FileVault para dispositivos Mac en su organización, consulte [Uso del cifrado de discos FileVault para macOS con Intune](../protect/encrypt-devices-filevault.md).  

## <a name="next-steps"></a>Pasos siguientes

Siempre puede recuperar la clave desde el sitio web del Portal de empresa, la aplicación de Intune y las aplicaciones Portal de empresa para iOS y Android, y usarla para acceder a su dispositivo Mac. Para obtener información sobre cómo recobrar la clave de recuperación, consulte [Obtención de una clave de recuperación para un dispositivo macOS](get-recovery-key-cpweb.md).

Descubra qué más puede hacer en el sitio web del Portal de empresa. Consulte [Usar el sitio web del Portal de empresa de Intune](using-the-intune-company-portal-website.md) para obtener la lista de acciones.  

¿Aún necesita ayuda? Póngase en contacto con el personal de soporte técnico de TI. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).