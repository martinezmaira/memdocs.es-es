---
title: Inscripción de un dispositivo Android con la aplicación Microsoft Intune y DISA Purebred
description: Obtenga información sobre cómo inscribir un dispositivo Android y cómo configurar la autenticación de credenciales derivadas con DISA Purebred.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 584392891320f96eed16863225ffb323dc240594
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880617"
---
# <a name="set-up-android-device-with-the-microsoft-intune-app-and-disa-purebred"></a>Configuración de un dispositivo Android con la aplicación Microsoft Intune y DISA Purebred

Inscriba el dispositivo con la aplicación de Microsoft Intune para obtener acceso seguro desde el móvil a las aplicaciones, los archivos y el correo electrónico de la organización. Después de haber inscrito el dispositivo, se convierte en *administrado*. La organización puede asignar directivas y aplicaciones al dispositivo mediante un proveedor de administración de dispositivos móviles (MDM), como Intune.  

Durante la inscripción, también instalará una credencial derivada en el dispositivo. La organización puede requerir que use la credencial derivada como método de autenticación al acceder a los recursos, o para firmar y cifrar mensajes de correo electrónico.

Es probable que necesite configurar una credencial derivada si usa una tarjeta inteligente para lo siguiente:

* Iniciar sesión en aplicaciones educativas o profesionales, Wi-Fi y redes privadas virtuales (VPN)
* Firmar y cifrar correos electrónicos educativos o profesionales con certificados S/MIME

En este artículo, aprenderá lo siguiente:

* Inscribir un dispositivo móvil Android con la aplicación de Intune.
* Configurar su tarjeta inteligente instalando una credencial derivada del proveedor de credenciales derivadas de su organización, [DISA Purebred](https://public.cyber.mil/pki-pke/purebred/)

## <a name="what-are-derived-credentials"></a>¿Qué son las credenciales derivadas?

Una credencial derivada es un certificado que se deriva de las credenciales de la tarjeta inteligente y que se instala en el dispositivo. Esta credencial concede acceso remoto a los recursos de trabajo, a la vez que evita que los usuarios no autorizados accedan a la información confidencial.

Las credenciales derivadas sirven para lo siguiente:

* Autenticar a los estudiantes y empleados que inician sesión en aplicaciones educativas o profesionales, Wi-Fi y en redes privadas virtuales (VPN)
* Firmar y cifrar correos electrónicos educativos o profesionales con certificados S/MIME

Las credenciales derivadas son una implementación de las directrices del National Institute of Standards and Technology (NIST) para las credenciales derivadas de verificación de identidad personal (PIV) como parte de la publicación especial (SP) 800-157.

## <a name="prerequisites"></a>Requisitos previos

Para completar la inscripción, debe tener lo siguiente:

* La tarjeta inteligente educativa o profesional que se le haya suministrado
* Acceso a un equipo o quiosco donde pueda iniciar sesión con la tarjeta inteligente
* Un dispositivo nuevo o restablecido a los valores de fábrica que ejecute Android 7.0 o una versión posterior 
* La aplicación de Microsoft Intune instalada en el dispositivo
* La aplicación Purebred instalada en el dispositivo (debe instalarse inmediatamente después de configurar el dispositivo; si no es así, póngase en contacto con el personal de soporte técnico de TI)

También será necesario ponerse en contacto con un agente o representante de Purebred durante la instalación.

## <a name="enroll-device"></a>Inscribir un dispositivo  

1. Encienda el dispositivo nuevo o restablecido de fábrica.  
2. En la pantalla **Bienvenida**, seleccione su idioma. Si se le ha indicado que se inscriba con un código QR o NFC, siga el paso siguiente que coincida con el método.  
     * NFC: coloque el dispositivo compatible con NFC contra un dispositivo de programador para conectarse a la red de la organización. Siga los mensajes en pantalla. Cuando llegue a la pantalla de los términos del servicio de Chrome, vaya al paso 5.  

     * Código QR: siga los pasos de [Inscripción de código QR](#qr-code-enrollment).  

     Si se le ha indicado que use otro método, vaya al paso 3.    

3. Conéctese a Wi-Fi y pulse **SIGUIENTE**. Siga el paso que coincide con el método de inscripción. 

    * Token: cuando llegue a la pantalla de inicio de sesión de Google, siga los pasos de [Inscripción de token](#token-enrollment).  
    * Google Zero Touch: después de conectarse a la Wi-Fi, la organización reconoce el dispositivo. Vaya al paso 4 y siga los mensajes en pantalla hasta que finalice la instalación.    
 
       ![Imagen de ejemplo de la pantalla de términos de Google que se ve si se usa Google Zero Touch con el botón Aceptar y continuar resaltado.](./media/google-zero-touch-intune-app-01.png)   
   
4. Revise los términos de Google. Luego pulse **ACEPTAR Y CONTINUAR**.  

      ![Imagen de ejemplo de la pantalla de términos de Google con el botón Aceptar y continuar resaltado.](./media/fully-managed-intune-app-04.png)   

5. Revise los términos del servicio de Chrome. Luego pulse **ACEPTAR Y CONTINUAR**.  

   ![Imagen de ejemplo de la pantalla de términos del servicio de Chrome con el botón Aceptar y continuar resaltado.](./media/fully-managed-intune-app-06.png)   

6. En la pantalla de inicio de sesión, pulse **Opciones de inicio de sesión** y, a continuación, **Iniciar sesión desde otro dispositivo**. 

7. Anote el código que aparece en pantalla.  

8. Cambie al dispositivo habilitado para tarjetas inteligentes y vaya a la dirección web que se muestra en la pantalla. 

9. Escriba el código que anotó anteriormente.

   > [!div class="mx-imgBorder"]
   > ![Captura de pantalla del mensaje "Introducir código" del sitio web de Portal de empresa.](./media/enter-code-intercede.png)

10. Inserte la tarjeta inteligente para iniciar sesión. 

11. En la pantalla de inicio de sesión, seleccione su cuenta profesional o educativa. A continuación, vuelva a su dispositivo móvil. 

12. Según los requisitos de la organización, es posible que se le pida que actualice la configuración, por ejemplo, el bloqueo de pantalla o el cifrado. Si ve estos mensajes, pulse **ESTABLECER** y siga las instrucciones en pantalla.  

       ![Imagen de ejemplo de configuración de la pantalla del teléfono profesional con el botón Establecer resaltado.](./media/fully-managed-intune-app-10.png)   

13. Para instalar aplicaciones profesionales en el dispositivo, pulse **INSTALAR**. Cuando termine la instalación, pulse **SIGUIENTE**.  

       ![Imagen de ejemplo de configuración de la pantalla del teléfono profesional con el botón Instalar resaltado.](./media/fully-managed-intune-app-11.png)   

14. Pulse **INICIAR** para abrir la aplicación Microsoft Intune. 

    ![Imagen de ejemplo de configuración de la pantalla del teléfono profesional con el botón Inicio resaltado.](./media/fully-managed-intune-app-17.png)   

15. Vuelva a la aplicación de Intune en el dispositivo móvil y siga las instrucciones en pantalla para inscribir el dispositivo. 

    ![Imagen de ejemplo de configuración del acceso: pantalla Registrar el dispositivo con el botón Listo resaltado](./media/fully-managed-intune-app-19.png)   

16. Continúe con la sección [Configuración de la tarjeta inteligente](enroll-android-device-disa-purebred.md#set-up-smart-card) de este artículo para terminar de configurar el dispositivo.  

### <a name="qr-code-enrollment"></a>Inscripción de código QR  
En esta sección se digitaliza el código QR proporcionado por la empresa.  Cuando termina, se le vuelve a redirigir a los pasos de inscripción del dispositivo.     
  
1. En la pantalla de **bienvenida**, pulse cinco veces para iniciar la configuración del código QR.  

   ![Imagen de ejemplo de la pantalla de bienvenida de instalación del dispositivo con las instrucciones de pulsar la pantalla resaltadas.](./media/qr-code-intune-app-01.png)  

2. Siga las instrucciones en pantalla para conectarse a Wi-Fi.  
3. Si el dispositivo no tiene un escáner de código QR, las pantallas de instalación muestran el progreso como un escáner en proceso de instalación. Espere a que la instalación se complete.  
4. Cuando se le pida, digitalice el código QR del perfil de inscripción que le ha proporcionado la organización.  
5. Vuelva al paso 4 de [Inscribir un dispositivo](#enroll-device) para continuar con la instalación.  

### <a name="token-enrollment"></a>Inscripción de token  
En esta sección se especifica el token proporcionado por la empresa. Cuando termina, se le vuelve a redirigir a los pasos de inscripción del dispositivo.  

1. En la pantalla de inicio de sesión de Google, en el cuadro **Correo electrónico o teléfono**, escriba **afw#setup**. Pulse **Siguiente**. 

   ![Imagen de ejemplo de la pantalla de inicio de sesión de Google con "afw#setup" escrito en el campo.](./media/token-intune-app-01.png)   

2. Seleccione **Instalar** para la aplicación **Android Device Policy** (Directiva de dispositivo Android). Continúe con la instalación. Según el dispositivo, es posible que deba revisar y aceptar más términos.    

3. En la pantalla **Inscribir este dispositivo**, seleccione **Siguiente**.  

4. Seleccione **Escribir código**.  

5. En la pantalla **Scan or enter code** (Digitalizar o escribir código), escriba el código que le ha proporcionado la organización.  A continuación, haga clic en **Siguiente**.  

   ![Imagen de ejemplo de la pantalla Scan or enter code (Digitalizar o escribir código) con el botón Siguiente resaltado.](./media/token-intune-app-04.png)  

6. Vuelva al paso 4 de [Inscribir un dispositivo](#enroll-device) para continuar con la instalación.


## <a name="set-up-smart-card"></a>Configuración de la tarjeta inteligente  

> [!NOTE]
> La aplicación Purebred es necesaria para completar estos pasos, y se instalará automáticamente en el dispositivo después de inscribirlo. Si, tras esperar unos instantes, sigue sin tener la aplicación, póngase en contacto con el personal de soporte técnico de TI.  

1. Una vez completada la inscripción, la aplicación de Intune le notificará para que configure la tarjeta inteligente. Pulse en la notificación. Si no recibe una notificación, consulte el correo electrónico.

   > [!div class="mx-imgBorder"]
   > ![Captura de pantalla de la notificación de inserción de la aplicación Intune en la pantalla de inicio del dispositivo](./media/action-required-in-app-android.png)

2. En la pantalla **Configurar la tarjeta inteligente**:

   1. Puntee el vínculo que lleva a las instrucciones de configuración de la organización y revíselas. Si la organización no proporciona instrucciones adicionales, se le enviará a este artículo.

   2. Puntee **COMENZAR**.   

   > [!div class="mx-imgBorder"]
   > ![Captura de pantalla de la pantalla Configurar la tarjeta inteligente de la aplicación Intune](./media/smart-card-open-disa-purebred-android.png)

3. En la pantalla **Obtener certificados**, puntee **INICIAR PUREBRED** para abrir la aplicación Purebred (esta aplicación debe haberse instalado automáticamente en el dispositivo; si no es así, póngase en contacto con el personal de soporte técnico).  

   > [!div class="mx-imgBorder"]
   > ![Captura de pantalla del mensaje de la aplicación Intune para abrir la aplicación DISA Purebred](./media/open-app-prompt-disa-purbred-android.png)  

4. Es posible que la aplicación Purebred necesite más permisos para ejecutarse correctamente. Puntee **Allow** (Permitir) o **Allow all the time** (Permitir todo el tiempo) cuando se le solicite. Para obtener más información sobre por qué estos permisos son necesarios, acuda a su contacto de soporte técnico o a su agente de Purebred.  

5. Una vez dentro de la aplicación Purebred, colabore con el agente de Purebred de su organización para descargar e instalar los certificados que son necesarios para acceder a los recursos profesionales o educativos.

    > [!IMPORTANT]
    > Durante este proceso, puntee **OK** (Aceptar) o **Install** (Instalar) cuando se le solicite. No cambie los nombres de ninguna entidad de certificación o certificado que deba instalar.    

6. Una vez completada la instalación, recibirá una notificación de que los certificados están listos. Puntee la notificación para volver a la aplicación Intune.

    > [!div class="mx-imgBorder"]
    > ![Captura de pantalla de la pantalla "Allow access to certificates" (Permitir el acceso a los certificados)](./media/certificates-ready-prompt-disa-purbred-android.png)

7. En la pantalla **Allow access to certificates** (Permitir el acceso a los certificados), configurará el permiso de aplicación Intune de forma que pueda acceder a las credenciales derivadas obtenidas de DISA Purebred. Con este paso se garantiza que la organización va a poder comprobar su identidad siempre que acceda a recursos profesionales o educativos protegidos.  

    1. Puntee **SIGUIENTE**.

       > [!div class="mx-imgBorder"]
       > ![Captura de pantalla que indica que los certificados están listos](./media/certificates-access-disa-purbred-android.png)

    2. Cuando se le pida que **elija certificado**, no cambie la selección; el certificado correcto ya está seleccionado, por lo que basta con puntear **Seleccionar** o **Aceptar**.  

       > [!div class="mx-imgBorder"]
       > ![Captura de pantalla del mensaje "Elegir certificado"](./media/choose-certificates-prompt-disa-purbred-android.png)

    3. La credencial derivada se compone de varios certificados, con lo cual el mensaje **Elegir certificado** aparecerá varias veces. Repita el paso anterior hasta que dejen de aparecer mensajes.  

8. Una vez procesados todos los certificados, espere a que la aplicación de Intune termine de configurar el dispositivo. Sabrá que la instalación se ha completado cuando vea el mensaje **¡Ya está todo listo!** en pantalla.  

    > [!div class="mx-imgBorder"]
    > ![Captura de pantalla de la pantalla "¡Ya está todo listo!"](./media/all-set-android.png)

## <a name="next-steps"></a>Pasos siguientes

Una vez completada la inscripción, tendrá acceso a los recursos de trabajo como, por ejemplo, correo electrónico, Wi-Fi y cualquier aplicación que la organización ponga a disposición de los usuarios. Para más información sobre cómo obtener, buscar, instalar y desinstalar aplicaciones en la aplicación de Intune, vea:

* [Usar aplicaciones administradas en el dispositivo](use-managed-apps-on-your-device-android.md)  
* [Administrar aplicaciones desde el sitio web del Portal de empresa](manage-apps-cpweb.md)  


¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
