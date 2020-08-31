---
title: Instalación de Mobile Threat Defense en su dispositivo móvil
description: Descubra qué son las aplicaciones de Mobile Threat Defense y cómo configurarlas.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: 23d449b6b5edf43ea709f8fce194ac5a8afe8eb4
ms.sourcegitcommit: 19ef60175cbfd5c5d1e213a6d64eded34ee42041
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/21/2020
ms.locfileid: "88725356"
---
# <a name="install-mobile-threat-defense-app"></a>Instalación de aplicaciones de Mobile Threat Defense  

> [!TIP]
> Hay una gran variedad de aplicaciones MTD en el mercado. Su organización debe indicarle cuál usar. Si se le pide que instale una aplicación MTD y no se le redirige inmediatamente para configurarla o instalarla, póngase en contacto con el personal de soporte técnico de TI para que le ayude.  

Como parte de los requisitos de seguridad de su organización, es posible que deba instalar una aplicación de proveedor de Mobile Threat Defense (MTD). Este tipo de aplicación detecta y comunica las amenazas presentes en el dispositivo, como aplicaciones sospechosas, redes o vulnerabilidades del sistema operativo.  

Si no tiene la aplicación MTD requerida, no podrá iniciar sesión en aplicaciones protegidas y administradas (como Microsoft Excel o OneDrive) con su cuenta profesional o educativa. En este artículo, aprenderá a [configurar una aplicación MTD](set-up-mobile-threat-defense.md#set-up-mtd-app) y a recuperar el acceso.    

## <a name="mtd-apps-for-ios"></a>Aplicaciones MTD para iOS
Las siguientes aplicaciones MTD se usan normalmente en dispositivos iOS. Seleccione una aplicación para abrir su lista en App Store.   

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## <a name="mtd-apps-for-android"></a>Aplicaciones MTD para Android 
Las siguientes aplicaciones MTD se usan normalmente en dispositivos Android. Seleccione una aplicación para abrir su lista en Google Play.  

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139454)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [Zimperium mobile IPS (zIPS)](https://go.microsoft.com/fwlink/?linkid=2139142)  


## <a name="information-your-organization-can-see"></a>Información que puede ver su organización   

Su organización no puede ver ningún dato, como textos, correos electrónicos e imágenes, en sus aplicaciones personales. La aplicación MTD informa sobre las aplicaciones, como el nombre y la versión, a su organización. La información real que se notifique dependerá del proveedor de MTD que use su empresa. Es posible que su organización vea lo siguiente:   

* Nombre de la aplicación  
* Id. de aplicación: nombre único que identifica a la aplicación en Google Play.  
* Versión de la aplicación y número de versión corto: números de versión específicos de una aplicación.  
* Lote de aplicaciones y tamaño dinámico: cantidad de espacio que usa una aplicación en el dispositivo. 


## <a name="set-up-mtd-app"></a>Configuración de la aplicación MTD 
Al iniciar sesión en una aplicación protegida, se le pedirá que instale una aplicación MTD. Siga los pasos en pantalla para completar la instalación y obtener acceso a la aplicación protegida. 

Para más información, consulte las instrucciones para [iOS](set-up-mobile-threat-defense.md#ios-setup) o [Android](set-up-mobile-threat-defense.md#android-setup) en esta sección. Estos pasos son complementarios y no pretenden reemplazar a las instrucciones que se muestran en pantalla. 

Si se le pide que instale una aplicación MTD, pero no está seguro de cuál, póngase en contacto con el personal de soporte técnico de TI para que le ayude.  

### <a name="device-registration"></a>Registro de dispositivos  
El registro de dispositivos es necesario para confirmar su identidad y conectar su cuenta profesional o educativa al dispositivo. Si el dispositivo no está registrado, se le guiará automáticamente por los pasos en pantalla, antes de instalar la aplicación MTD.   

Para obtener más información sobre el registro de dispositivos, vea [Registro de su dispositivo personal en la red de su organización](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>Configuración de iOS  
Estos pasos comienzan en la pantalla **Obtener acceso**, que aparece después de iniciar sesión en una aplicación protegida.  

1. En la pantalla **Obtener acceso**, siga las instrucciones para instalar la aplicación MTD requerida por su organización.   
2. Vuelva a la pantalla **Obtener acceso** y seleccione **Abrir**.  
3. La aplicación MTD solicita permiso para abrir Microsoft Authenticator. Seleccione **Abrir**. 
4. Seleccione su cuenta profesional para iniciar sesión. 
5. Espere mientras la aplicación MTD examina el dispositivo en busca de amenazas de seguridad. 
6. Vuelva a la aplicación educativa o de trabajo a la que estaba intentando acceder inicialmente. En este punto, su organización podría pedirle que configurase otros requisitos de seguridad de la aplicación, como un PIN.   
7. Ahora debería tener acceso a la aplicación. Si todavía está bloqueado:  
    * En la pantalla **Obtener acceso**, seleccione **Volver a comprobar**.  
    * Vaya a la aplicación MTD y compruebe si hay amenazas existentes. Complete los pasos recomendados para resolver la amenaza y recuperar el acceso.    

### <a name="android-setup"></a>Configuración de Android 
Estos pasos comienzan en la pantalla **Obtener acceso**, que aparece después de iniciar sesión en una aplicación protegida.  

1. En la pantalla **Obtener acceso**, siga las instrucciones para instalar la aplicación MTD requerida por su organización.  
2. Vuelva a la pantalla **Obtener acceso** y seleccione **Abrir**.  
3. La aplicación MTD solicita permiso para acceder a determinadas áreas del dispositivo, en caso de que sea necesario. Para que esta aplicación funcione correctamente, debe **permitir** el acceso a los contactos. Los permisos solicitados variarán en los proveedores de MTD.  
4. Seleccione su cuenta profesional para iniciar sesión.  
5. Espere mientras la aplicación MTD examina el dispositivo en busca de amenazas de seguridad.  
6. Vuelva a la aplicación educativa o de trabajo a la que estaba intentando acceder inicialmente. En este punto, su organización podría pedirle que configurase otros requisitos de seguridad de la aplicación, como un PIN.  
7. Ahora debería tener acceso a la aplicación. Si todavía está bloqueado:  
    * En la pantalla **Obtener acceso**, seleccione **Volver a comprobar**.  
    * Vaya a la aplicación MTD y compruebe si hay amenazas existentes. Complete los pasos recomendados para resolver la amenaza y recuperar el acceso.  


## <a name="resolving-a-threat"></a>Resolución de una amenaza
Si se detecta una amenaza que supera el nivel definido por la organización, la organización podrá:  
   
* Bloquear acceso: impide que use las aplicaciones protegidas de su organización mientras tenga la sesión iniciada con su cuenta profesional o educativa.  
* Borrar datos: elimina los datos profesionales o educativos de una o varias aplicaciones protegidas de su organización.  

Para resolver una amenaza y recuperar el acceso a las aplicaciones protegidas:  

1. Abra la aplicación MTD en su dispositivo.     
2. Lea los detalles de la amenaza en la aplicación, que explica cómo la amenaza podría afectar al dispositivo si se deja sin resolver y cómo hacerlo. 
3. Después de realizar los cambios necesarios en el dispositivo, vuelva a la aplicación MTD e inicie un nuevo examen. Repita estos pasos hasta que se resuelvan todas las amenazas. Los cambios pueden tardar unos minutos en sincronizarse con su organización. Una vez que se sincronicen los cambios, recuperará el acceso a la aplicación protegida. 

## <a name="get-support"></a>Obtención de soporte técnico
Vaya al [sitio web Portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980) para buscar la información de contacto de su empresa. Póngase en contacto con ellos para obtener ayuda con:

* Identificación de la aplicación MTD que se va a usar  
* Instalación  
* Error de instalación  
* Detección y resolución de amenazas  
* Desinstalación de una aplicación MTD   
 

### <a name="share-app-logs-with-it-support"></a>Compartir registros de aplicaciones con el personal de soporte técnico de TI  
También puede enviar los registros de aplicaciones al personal de soporte técnico de TI para proporcionarles más contexto sobre una instalación con errores.  
* Usuarios de Android: [Cargue y envíe por correo electrónico los registros](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) desde Portal de empresa.   

* Usuarios de dispositivos iOS: [Recupere y envíe los registros](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) desde Microsoft Edge para iOS.  


## <a name="next-steps"></a>Pasos siguientes  

Consulte los artículos siguientes para saber cómo funcionan las aplicaciones administradas, cómo obtenerlas y cómo reconocer que está usando una.  

* [Usar aplicaciones administradas en el dispositivo Android](use-managed-apps-on-your-device-android.md)
* [Usar aplicaciones administradas en el dispositivo iOS](use-managed-apps-on-your-device-ios.md)  

¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).

