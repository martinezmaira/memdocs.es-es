---
title: Inscripción de un dispositivo Android con Portal de empresa de Intune e Intercede
description: Inscriba un dispositivo Android y configure la autenticación de credenciales derivadas con Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8afc499f85e91658b411a25988ac858ca59030cc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81616052"
---
# <a name="set-up-android-device-with-company-portal-and-intercede"></a>Configuración de un dispositivo Android con Portal de empresa e Intercede

Inscriba el dispositivo con la aplicación Portal de empresa de Intune para obtener acceso seguro desde el móvil a las aplicaciones, los archivos y el correo electrónico de la organización. Después de haber inscrito el dispositivo, se convierte en *administrado*. La organización puede asignar directivas y aplicaciones al dispositivo mediante un proveedor de administración de dispositivos móviles (MDM), como Intune.

Durante la inscripción, también instalará una credencial derivada en el dispositivo. La organización puede requerir que use la credencial derivada como método de autenticación al acceder a los recursos, o para firmar y cifrar mensajes de correo electrónico.

Es probable que necesite configurar una credencial derivada si usa una tarjeta inteligente para lo siguiente:

* Iniciar sesión en aplicaciones educativas o profesionales, Wi-Fi y redes privadas virtuales (VPN)
* Firmar y cifrar correos electrónicos educativos o profesionales con certificados S/MIME

En este artículo, aprenderá lo siguiente:

* Inscribir un dispositivo móvil Android con Portal de empresa de Intune.
* Configurar su tarjeta inteligente mediante la instalación de una credencial derivada del proveedor de credenciales derivadas de su organización, [Intercede](https://www.intercede.com/).  

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

16. Continúe con la sección [Configuración de la tarjeta inteligente](enroll-android-device-intercede.md#set-up-smart-card) de este artículo para terminar de configurar el dispositivo.  

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

1. Una vez completada la inscripción, la aplicación de Intune le notificará para que configure la tarjeta inteligente. Pulse en la notificación. Si no recibe una notificación, consulte el correo electrónico.

   > [!div class="mx-imgBorder"]
   > ![Captura de pantalla de ejemplo de la notificación de inserción de Portal de empresa en la pantalla de inicio del dispositivo.](./media/action-required-in-app-android.png)

2. En la pantalla **Configurar la tarjeta inteligente**:

   1. Pulse el vínculo que lleva a las instrucciones de configuración de la organización. Si la organización no proporciona instrucciones adicionales, se le enviará a este artículo.

   2. Pulse **Comenzar**.  

   > [!div class="mx-imgBorder"]
   > ![Captura de pantalla de ejemplo de la pantalla "Configurar el acceso a la tarjeta inteligente móvil" de Portal de empresa.](./media/smart-card-open-entrust-android.png)

3. Cambie al dispositivo habilitado para tarjeta inteligente o al quiosco de autoservicio y abra la aplicación MyID. Inicie sesión con sus credenciales profesionales.

4. Seleccione la opción para solicitar un identificador.

5. Cuando se le pregunte qué perfil quiere usar, seleccione la opción para activar con una credencial móvil. Aparece un código QR.  

6. Vuelva a su dispositivo Android. En la pantalla **Obtener un código QR** de Portal de empresa, pulse **Siguiente**.

    > [!div class="mx-imgBorder"]
    > ![Captura de pantalla de ejemplo de la pantalla "Obtener un código QR" de Portal de empresa.](./media/get-qr-code-entrust-android.png)

7. Si se le pide que permita que la aplicación de Intune use la cámara, pulse **Permitir**.

8. Escanee la imagen de código QR que hay en su dispositivo habilitado para tarjeta inteligente.

9. La aplicación de Intune iniciará la descarga e instalación de los certificados necesarios para acceder a los recursos profesionales o educativos. En función de su conexión a Internet, este proceso puede tardar algún tiempo en completarse. No cierre la aplicación durante este período de tiempo.

    > [!div class="mx-imgBorder"]
    > ![Captura de pantalla de ejemplo de la pantalla "Descargando e instalando certificados" de Portal de empresa](./media/install-certificates-entrust-android.png)

10. Una vez procesados todos los certificados, espere a que la aplicación de Intune termine de configurar el dispositivo. Sabrá que la instalación se ha completado cuando vea el mensaje **¡Ya está todo listo!** en pantalla.

    > [!div class="mx-imgBorder"]
    > ![Captura de pantalla de ejemplo de la pantalla "¡Ya está todo listo!"](./media/all-set-android.png)

## <a name="next-steps"></a>Pasos siguientes

Una vez completada la inscripción, tendrá acceso a los recursos de trabajo como, por ejemplo, correo electrónico, Wi-Fi y cualquier aplicación que la organización ponga a disposición de los usuarios. Para más información sobre cómo obtener, buscar, instalar y desinstalar aplicaciones en la aplicación de Intune, vea:

* [Usar aplicaciones administradas en el dispositivo](use-managed-apps-on-your-device-android.md)  
* [Administrar aplicaciones desde el sitio web del Portal de empresa](manage-apps-cpweb.md)  

¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
