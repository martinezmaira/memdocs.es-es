---
title: Inscripción de un dispositivo iOS o iPadOS con Portal de empresa de Intune y Entrust Datacard
description: Inscriba un dispositivo iOS o iPadOS y configure la autenticación de credenciales derivadas con Entrust Datacard.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
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
ms.openlocfilehash: 1e1f1c04bed91de3ac193ea3b6a07bde4e8658ba
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81638245"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>Configuración de un dispositivo iOS o iPadOS con Portal de empresa de Intune y Entrust Datacard

Inscriba el dispositivo con la aplicación Portal de empresa de Intune para obtener acceso seguro desde el móvil a las aplicaciones, los archivos y el correo electrónico de la organización. Después de haber inscrito el dispositivo, se convierte en *administrado*. La organización puede asignar directivas y aplicaciones al dispositivo mediante un proveedor de administración de dispositivos móviles (MDM), como Intune.  

Durante la inscripción, también instalará una credencial derivada en el dispositivo. La organización puede requerir que use la credencial derivada como método de autenticación al acceder a los recursos, o para firmar y cifrar mensajes de correo electrónico. 

Es probable que necesite configurar una credencial derivada si usa una tarjeta inteligente para lo siguiente:  

* Iniciar sesión en aplicaciones educativas o profesionales, Wi-Fi y redes privadas virtuales (VPN)
* Firmar y cifrar correos electrónicos educativos o profesionales con certificados S/MIME  

En este artículo, aprenderá lo siguiente:  

   * Inscribir un dispositivo iOS o iPadOS con Portal de empresa de Intune  
   * Obtener una credencial derivada del proveedor de credenciales derivadas de la organización, [Entrust Datacard](https://www.entrustdatacard.com/)  

### <a name="what-are-derived-credentials"></a>¿Qué son las credenciales derivadas?  
Una credencial derivada es un certificado que se deriva de las credenciales de la tarjeta inteligente y que se instala en el dispositivo. Esta credencial concede acceso remoto a los recursos de trabajo, a la vez que evita que los usuarios no autorizados accedan a la información confidencial.  

Las credenciales derivadas sirven para lo siguiente: 
* Autenticar a los estudiantes y empleados que inician sesión en aplicaciones educativas o profesionales, Wi-Fi y en redes privadas virtuales (VPN)
* Firmar y cifrar correos electrónicos educativos o profesionales con certificados S/MIME

Las credenciales derivadas son una implementación de las directrices del National Institute of Standards and Technology (NIST) para las credenciales derivadas de verificación de identidad personal (PIV) como parte de la publicación especial (SP) 800-157.  

## <a name="prerequisites"></a>Requisitos previos

 Para completar la inscripción, debe tener lo siguiente:

* La tarjeta inteligente educativa o profesional que se le haya suministrado
* Acceso a un equipo o quiosco donde pueda iniciar sesión con la tarjeta inteligente
* El dispositivo móvil
* La aplicación Portal de empresa de Intune para iOS y iPadOS instalada en el dispositivo  


## <a name="enroll-device"></a>Inscribir un dispositivo  
1. Abra la aplicación Portal de empresa para iOS/iPadOS en el dispositivo móvil e inicie sesión con su cuenta profesional.  

2. Anote el código que aparece en pantalla.  

    ![Imagen de ejemplo de la aplicación Portal de empresa con un mensaje en pantalla y un código](./media/copy-code-intercede.png)   

3. Cambie al dispositivo habilitado para tarjeta inteligente y vaya a https://microsoft.com/devicelogin. 
4. Escriba el código que anotó anteriormente.  

    ![Captura de pantalla de ejemplo del mensaje "Introducir código" del sitio web de Portal de empresa](./media/enter-code-intercede.png)   

5. Inserte la tarjeta inteligente para iniciar sesión.   
6. Vuelva a la aplicación Portal de empresa en el dispositivo móvil y siga las instrucciones en pantalla para inscribir el dispositivo.  
7. Una vez completada la inscripción, Portal de empresa le notificará para que configure la tarjeta inteligente. Pulse en la notificación. Si no recibe una notificación, consulte el correo electrónico.   

    ![Captura de pantalla de ejemplo de la notificación de inserción de Portal de empresa en la pantalla de inicio del dispositivo](./media/action-required-in-app-intercede.png)  

8. En la pantalla **Configurar el acceso a la tarjeta inteligente móvil**:   
    a. Pulse el vínculo que lleva a las instrucciones de configuración de la organización. Si la organización no proporciona instrucciones adicionales, se le enviará a este artículo.  
    b. Pulse **Comenzar**.  

    ![Captura de pantalla de ejemplo de la pantalla Configurar el acceso a la tarjeta inteligente móvil de Portal de empresa](./media/smart-card-info-intercede.png)

9. Cambie al dispositivo habilitado para tarjeta inteligente y abra IdentityGuard. 
10. Busque el área de inicio de sesión con credencial inteligente y seleccione el botón de inicio de sesión.  
11. Cuando se le pida que seleccione un certificado, elija sus credenciales de tarjeta inteligente. Luego, seleccione **Aceptar**. 
12. Escriba el PIN de su tarjeta inteligente.  
13. Se le pedirá que elija de entre una lista de acciones. Seleccione la que le permita inscribirse para una credencial inteligente móvil derivada. El vínculo o el botón podrían indicar algo así como **Me gustaría inscribirme para obtener una credencial de tarjeta inteligente móvil derivada**.  
14. Seleccione que ha descargado e instalado correctamente la aplicación habilitada para credencial inteligente. Luego, avance a la siguiente pantalla.   
15. Escriba información sobre su credencial de tarjeta inteligente derivada.  
    a. Escriba lo que quiera como nombre de identidad, por ejemplo, *Cred. derivada de Entrust*.  
    b. En el menú desplegable, seleccione **Credencial inteligente de Entrust IdentityGuard Mobile**.  
    c. Avance a la siguiente pantalla. Verá un código QR con una contraseña numérica debajo.  

16. Vuelva al dispositivo móvil. En Portal de empresa > pantalla **Obtener un código QR**, pulse **Continuar**. 

    ![Captura de pantalla de ejemplo de la pantalla Obtener un código QR de Portal de empresa](./media/get-qr-code-intercede.png)  
17. Pulse **Usar cámara** > **Aceptar**.  

    ![Captura de pantalla de ejemplo de un mensaje de Portal de empresa en el que se pide permiso para acceder a la cámara](./media/allow-cp-camera-access-intercede.png)  
18. Escanee la imagen de código QR que hay en su dispositivo habilitado para tarjeta inteligente.  
19. Escriba la contraseña numérica que aparece debajo del código QR.  

    ![Captura de pantalla de ejemplo de la pantalla Se requiere contraseña de Portal de empresa, con el campo para escribir la contraseña](./media/enter-password-derived-credentials.png)   

20. Espere a que Portal de empresa termine de configurar el dispositivo.  


## <a name="next-steps"></a>Pasos siguientes  
Una vez completada la inscripción, tendrá acceso a los recursos de trabajo como, por ejemplo, correo electrónico, Wi-Fi y cualquier aplicación que la organización ponga a disposición de los usuarios. Para obtener más información sobre cómo obtener, buscar, instalar y desinstalar aplicaciones en Portal de empresa, vea:

* [Administrar aplicaciones desde el sitio web del Portal de empresa](manage-apps-cpweb.md)  
* [Usar aplicaciones administradas en el dispositivo](use-managed-apps-on-your-device-ios.md)  

¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  
