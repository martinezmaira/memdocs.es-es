---
title: Inscripción de un dispositivo iOS o iPadOS con Portal de empresa de Intune e Intercede
description: Obtenga información sobre cómo inscribir un dispositivo iOS o iPadOS y cómo configurar la autenticación de credenciales derivadas con Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: bac9edcb91ef49cfa2252bd82e6e88bfd512d9ef
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881516"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>Configuración de un dispositivo iOS o iPadOS con Portal de empresa de Intune y Intercede

Inscriba el dispositivo con la aplicación Portal de empresa de Intune para obtener acceso seguro desde el móvil a las aplicaciones, los archivos y el correo electrónico de la organización.  Después de haber inscrito el dispositivo, se convierte en *administrado*. La organización puede asignar directivas y aplicaciones al dispositivo mediante un proveedor de administración de dispositivos móviles (MDM), como Intune.  

Durante la inscripción, también instalará una credencial derivada en el dispositivo. La organización puede requerir que use la credencial derivada como método de autenticación al acceder a los recursos, o para firmar y cifrar mensajes de correo electrónico. 

Es probable que necesite configurar una credencial derivada si usa una tarjeta inteligente para lo siguiente:

* Iniciar sesión en aplicaciones educativas o profesionales, Wi-Fi y redes privadas virtuales (VPN)
* Firmar y cifrar correos electrónicos educativos o profesionales con certificados S/MIME  

En este artículo, aprenderá lo siguiente:  

* Inscribir un dispositivo iOS o iPadOS con Portal de empresa de Intune  
* Obtener una credencial derivada del proveedor de credenciales derivadas de la organización, [Intercede](https://www.intercede.com/)   


## <a name="what-are-derived-credentials"></a>¿Qué son las credenciales derivadas?  
Una credencial derivada es un certificado que se deriva de las credenciales de la tarjeta inteligente y que se instala en el dispositivo. Esta credencial concede acceso remoto a los recursos de trabajo, a la vez que evita que los usuarios no autorizados accedan a la información confidencial.  

Las credenciales derivadas sirven para lo siguiente: 
* Autenticar a los estudiantes y empleados que inician sesión en aplicaciones educativas o profesionales, Wi-Fi y en redes privadas virtuales (VPN)
* Firmar y cifrar correos electrónicos educativos o profesionales con certificados S/MIME  

Las credenciales derivadas son una implementación de las directrices del National Institute of Standards and Technology (NIST) para las credenciales derivadas de verificación de identidad personal (PIV) como parte de la publicación especial (SP) 800-157.  

## <a name="prerequisites"></a>Requisitos previos

 Para completar la inscripción, debe tener lo siguiente:

* La tarjeta inteligente educativa o profesional que se le haya suministrado
* Acceso a un equipo o quiosco de autoservicio donde pueda iniciar sesión con la tarjeta inteligente
* Dispositivo móvil
* La aplicación Portal de empresa de Intune para iOS y iPadOS instalada en el dispositivo


## <a name="enroll-device"></a>Inscribir un dispositivo  
1. Abra la aplicación Portal de empresa para iOS/iPadOS en el dispositivo móvil e inicie sesión con su cuenta profesional.  
2. Anote el código que aparece en la pantalla.  

    ![Imagen de ejemplo de la aplicación Portal de empresa con un mensaje en pantalla y un código](./media/copy-code-intercede.png)  
1. Cambie al dispositivo habilitado para tarjeta inteligente y vaya a https://microsoft.com/devicelogin. 

1. Escriba el código que anotó anteriormente.
 
2. Inserte la tarjeta inteligente para iniciar sesión.   

3. Vuelva a la aplicación Portal de empresa en el dispositivo móvil y siga las instrucciones en pantalla para inscribir el dispositivo.  
4. Una vez completada la inscripción, Portal de empresa le notificará para que configure la tarjeta inteligente. Pulse en la notificación. Si no recibe una notificación, consulte el correo electrónico.   

    ![Captura de pantalla de ejemplo de la notificación de inserción de Portal de empresa en la pantalla de inicio del dispositivo](./media/action-required-in-app-intercede.png)  

5. En la pantalla **Configurar el acceso a la tarjeta inteligente móvil**:  
    a. Pulse el vínculo que lleva a las instrucciones de configuración de la organización. Si la organización no proporciona instrucciones adicionales, se le enviará a este artículo.  
    b. Pulse **Comenzar**.  

    ![Captura de pantalla de ejemplo de la pantalla Configurar el acceso a la tarjeta inteligente móvil de Portal de empresa](./media/smart-card-info-intercede.png)  

6. Cambie al dispositivo habilitado para tarjeta inteligente o al quiosco de autoservicio y abra la aplicación MyID. Inicie sesión con sus credenciales profesionales.  
7. Seleccione la opción para solicitar un identificador. 
8. Cuando se le pregunte qué perfil quiere usar, seleccione la opción para activar con una credencial móvil. Aparece un código QR.  
9. Vuelva al dispositivo móvil. En Portal de empresa > pantalla **Obtener un código QR**, pulse **Continuar**.  

    ![Captura de pantalla de ejemplo de la pantalla Obtener un código QR de Portal de empresa](./media/get-qr-code-intercede.png) 
 
10. Pulse **Usar cámara** > **Aceptar**.  

    ![Captura de pantalla de ejemplo de un mensaje de Portal de empresa en el que se pide permiso para acceder a la cámara](./media/allow-cp-camera-access-intercede.png)  

11. Escanee la imagen de código QR que hay en su dispositivo habilitado para tarjeta inteligente. 
12. Espere a que Portal de empresa termine de configurar el dispositivo.  

## <a name="next-steps"></a>Pasos siguientes  
Una vez completada la inscripción, tendrá acceso a los recursos de trabajo como, por ejemplo, correo electrónico, Wi-Fi y cualquier aplicación que la organización ponga a disposición de los usuarios. Para obtener más información sobre cómo obtener, buscar, instalar y desinstalar aplicaciones en Portal de empresa, vea:

* [Administrar aplicaciones desde el sitio web del Portal de empresa](manage-apps-cpweb.md)  
* [Usar aplicaciones administradas en el dispositivo](use-managed-apps-on-your-device-ios.md)  

¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
