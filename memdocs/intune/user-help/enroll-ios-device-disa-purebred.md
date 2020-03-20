---
title: Inscripción de un dispositivo iOS o iPadOS con Portal de empresa de Intune y DISA Purebred
description: Obtenga información sobre cómo inscribir un dispositivo iOS o iPadOS y cómo configurar la autenticación de credenciales derivadas con DISA Purebred.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 38d1b40ecdeee5bfd872297a5fd4f0229cb48dcf
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337595"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>Configuración de un dispositivo iOS o iPadOS con Portal de empresa de Intune y DISA Purebred  

Inscriba el dispositivo con la aplicación Portal de empresa de Intune para obtener acceso seguro desde el móvil a las aplicaciones, los archivos y el correo electrónico de la organización. Después de haber inscrito el dispositivo, se convierte en *administrado*. La organización puede asignar directivas y aplicaciones al dispositivo mediante un proveedor de administración de dispositivos móviles (MDM), como Intune.  

Durante la inscripción, también instalará una credencial derivada en el dispositivo. La organización puede requerir que use la credencial derivada como método de autenticación al acceder a los recursos, o para firmar y cifrar mensajes de correo electrónico. 

Es probable que necesite configurar una credencial derivada si usa una tarjeta inteligente para lo siguiente:

* Iniciar sesión en aplicaciones educativas o profesionales, Wi-Fi y redes privadas virtuales (VPN)
* Firmar y cifrar correos electrónicos educativos o profesionales con certificados S/MIME  

En este artículo, aprenderá lo siguiente:  

   * Inscribir un dispositivo iOS o iPadOS con Portal de empresa de Intune  
   * Obtener una credencial derivada del proveedor de credenciales derivadas de la organización, [DISA Purebred](https://cyber.mil/pki-pke/purebred/)  

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
* El dispositivo móvil
* La aplicación Portal de empresa de Intune para iOS y iPadOS instalada en el dispositivo   

También será necesario ponerse en contacto con un agente o representante de Purebred durante la instalación.      

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
    b. Haga clic en **Abrir** para abrir la aplicación Purebred.  

    ![Captura de pantalla de ejemplo de la pantalla Configurar el acceso a la tarjeta inteligente móvil de Portal de empresa](./media/smart-card-open-disa-purebred.png)  
9. Cuando se le pida que permita a Portal de empresa abrir la aplicación de registro de Purebred, seleccione **Abrir**.   

    ![Captura de pantalla de ejemplo del mensaje de Portal de empresa para abrir la aplicación DISA Purebred](./media/open-app-prompt-disa-purbred.png)  
10. Cuando la aplicación funcione, acuda al agente de Purebred de la organización para configurar y descargar el perfil de configuración de inscripción previa de Purebred.   
11. Vaya a la aplicación Settings > **General** > **Profiles & Device Management** > **Install Profile** (Configuración > General > Perfiles y administración de dispositivos > Instalar perfil) y pulse **Install** (Instalar).  
12. Escriba el código de acceso del dispositivo.  
13. Instale el perfil. Es posible que tenga que pulsar **Install** (Instalar) más de una vez para iniciar la instalación. 
14. Vuelva a la aplicación de registro de Purebred. Siga las instrucciones del agente de Purebred para continuar.  
 
15. Tras descargar el perfil de configuración, vaya a la aplicación Settings > **General** > **Profiles & Device Management** > **Install Profile** (Configuración > General > Perfiles y administración de dispositivos > Instalar perfil) y pulse **Install** (Instalar).   
16.  Escriba el código de acceso del dispositivo.
17. Instale el perfil. Es posible que tenga que pulsar **Install** (Instalar) más de una vez para iniciar la instalación. 
18. Una vez finalizada la instalación, vuelva a la aplicación Portal de empresa.  
19.  En la pantalla **Configurar el acceso a la tarjeta inteligente móvil** pulse **Continuar**.  

20. En la pantalla **Importar los certificados**, recuperará e importará la credencial derivada que recibió de DISA Purebred.  

    a. Pulse **Continuar**.   

    ![Captura de pantalla de ejemplo de la pantalla Importar los certificados de Portal de empresa](./media/import-certificate-disa-purebred.png)  
    b. Vaya a iCloud Drive, a **Browse** > **Locations** (Examinar > Ubicaciones), y pulse **More locations** (Más ubicaciones).  

    ![Captura de pantalla de ejemplo del menú Browse (Examinar) de iCloud Drive con la opción More locations (Más ubicaciones) resaltada](./media/icloud-drive-more-locations.png)  
    c. Pulse el conmutador para habilitar **Purebred Key Chain** (Cadena de claves de Purebred).  

    ![Captura de pantalla de ejemplo de la vista Browse (Examinar) de iCloud Drive, donde se resalta que el conmutador Purebred Key Chain (Cadena de claves de Purebred) está habilitado](./media/icloud-drive-enable-purebred-keychain.png)   

    d. Pulse **Purebred Credential Package** (Paquete de credenciales de Purebred).  

    ![Captura de pantalla de ejemplo de una pantalla de iOS con una opción Purebred Credential Package (Paquete de credenciales de Purebred) seleccionable](./media/purebred-credential-package.png)  
    f. Aparece una lista de certificados. Seleccione uno y pulse **Import key** (Importar clave).  

    ![Captura de pantalla de ejemplo de una lista de certificados seleccionables, con uno ya seleccionado](./media/import-purebred-keychain.png) 
21. Vuelva a la aplicación Portal de empresa y espere a que Portal de empresa termine de configurar el dispositivo.   

## <a name="next-steps"></a>Pasos siguientes  
Una vez completada la inscripción, tendrá acceso a los recursos de trabajo como, por ejemplo, correo electrónico, Wi-Fi y cualquier aplicación que la organización ponga a disposición de los usuarios. Para obtener más información sobre cómo obtener, buscar, instalar y desinstalar aplicaciones en Portal de empresa, vea:

* [Administrar aplicaciones desde el sitio web del Portal de empresa](manage-apps-cpweb.md)  
* [Usar aplicaciones administradas en el dispositivo](use-managed-apps-on-your-device-ios.md)  

¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
