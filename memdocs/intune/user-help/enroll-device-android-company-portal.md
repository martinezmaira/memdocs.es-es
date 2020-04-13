---
title: Inscribir dispositivos Android con Portal de empresa de Intune | Microsoft Docs
description: Explica cómo inscribir un dispositivo Android con Portal de empresa de Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/01/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 0c9bf96188e27afeaf66e7b2897f8cda19f9df37
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551653"
---
# <a name="enroll-your-device-with-company-portal"></a>Inscribir dispositivos con Portal de empresa  
Inscriba el dispositivo corporativo o personal Android para obtener acceso seguro al correo electrónico, las aplicaciones y los datos corporativos. Portal de empresa admite dispositivos Android, incluido Samsung Knox, con Android 4.4 y posterior.  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung Knox es un tipo de seguridad que usan determinados dispositivos Samsung para lograr una protección adicional a la ofrecida por Android de forma nativa. Para comprobar si tiene un dispositivo Samsung Knox, vaya a **Configuración** > **Acerca del dispositivo**. Si no ve **Versión Knox** en la lista, tiene un dispositivo Android nativo.

## <a name="enroll-device"></a>Inscribir un dispositivo  
Asegúrese de [instalar la aplicación Portal de empresa de Intune desde Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). Consulte [Instalación de la aplicación Portal de empresa en la China continental](install-company-portal-android-china.md) para obtener una lista de tiendas que ofrecen la aplicación en la China continental.    

Durante la inscripción, es posible que se le pida que elija la categoría que mejor describa la forma en que usa el dispositivo. El equipo de soporte técnico de la empresa usa la respuesta para comprobar las aplicaciones a las que se tiene acceso.  

1. Abra la aplicación Portal de empresa e inicie sesión con su cuenta profesional o educativa.  

2. Si se le pide que acepte los términos y condiciones de la organización, pulse **ACEPTAR TODO**.  

   ![Imagen de ejemplo de la pantalla Términos de Portal de empresa con el botón "Aceptar todo" resaltado](./media/accept-terms-1911.png)  


3. Revise lo que su organización puede y no puede ver. Después, pulse **CONTINUAR**.


    ![Imagen de ejemplo de Portal de empresa, pantalla Nos preocupamos por su privacidad, con el botón Continuar resaltado.](./media/android-privacy-screen-1911.png)  
4. Revise lo que va a suceder en los próximos pasos y, luego, pulse **SIGUIENTE**.  

    ![Imagen de ejemplo de la pantalla ¿Cuál es el paso siguiente? de Portal de empresa con botón Siguiente resaltado](./media/android-whats-next-1911.png)  


5. En función de la versión de Android, es posible que se le pida que permita el acceso a determinadas partes del dispositivo. Estos mensajes proceden de Google y no están bajo control de Microsoft.  

    Pulse **Permitir** en los siguientes permisos:  
    * **Permitir al Portal de empresa hacer llamadas telefónicas y administrarlas**: este permiso permite al dispositivo compartir su número de identidad internacional de equipo móvil (IMEI) con Intune, el proveedor de administración de dispositivos de la organización. Este permiso se puede permitir con total seguridad. Microsoft nunca realizará ni administrará llamadas telefónicas.  
    * **Permitir al Portal de empresa acceder a sus Contactos**: con este permiso, la aplicación Portal de empresa puede crear, usar y administrar su cuenta profesional.  Este permiso se puede permitir con total seguridad. Microsoft nunca accederá a sus contactos. 

    Si deniega el permiso, se le pedirá de nuevo la próxima vez que inicie sesión en Portal de empresa. Para desactivar estos mensajes, seleccione **No volver a preguntar**. Para administrar los permisos de la aplicación, vaya a la aplicación Configuración > **Aplicaciones** > **Portal de empresa** > **Permisos** > **Teléfono**.  

6. Active la aplicación de administración de dispositivos. 

    Portal de empresa necesita permisos de administrador de dispositivos para administrar el dispositivo de forma segura. La activación de la aplicación permite a la organización identificar posibles problemas de seguridad (como los intentos fallidos de desbloqueo del dispositivo) y reaccionar del modo adecuado.  

    ![Imagen de ejemplo de la pantalla de activación de la aplicación de administración de dispositivos con el botón de activación resaltado](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft no controla los mensajes de esta pantalla. Sabemos que están redactados de forma bastante contundente. Portal de empresa no pueden especificar qué restricciones y accesos son relevantes en su organización. Si tiene alguna pregunta sobre cómo se usa esta aplicación en su organización, póngase en contacto con el personal de soporte técnico de TI. Vaya al [sitio web Portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980) para buscar la información de contacto de su empresa.  


7. Se inicia la inscripción del dispositivo. Si usa un dispositivo Samsung Knox, primero se le pedirá que revise y acepte la directiva de privacidad del agente ELM.   

    ![Imagen de ejemplo de la pantalla de directiva de privacidad de Samsung Knox que aparece durante la inscripción](./media/and-enroll-7-knox-privacy-policy.png)  

8. En la pantalla **Configuración de acceso a la empresa**, compruebe que el dispositivo está inscrito. Después, pulse **CONTINUAR**.  

    ![Imagen de ejemplo de la pantalla Configuración de acceso a la empresa de Portal de empresa en la que se muestra que "Tenga su dispositivo administrado" se ha completado](./media/update-settings-1911.png)  

9. Es posible que su organización requiera que actualice la configuración del dispositivo. Pulse **RESOLVER** para ajustar una configuración. Cuando haya terminado de actualizar la configuración, pulse **CONTINUAR**.  

   ![Imagen de ejemplo de la pantalla Actualizar configuración del dispositivo de Portal de empresa con los botones Resolver y Continuar resaltados](./media/resolve-settings-1911.png)  

10. Una vez finalizada la instalación, pulse **LISTO**.    

    ![Imagen de ejemplo de Portal de empresa, pantalla Configuración de acceso a la empresa, en la que se muestra la configuración completa y el botón Listo resaltado.](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>Pasos siguientes  

Antes de intentar instalar una aplicación educativa o profesional, vaya a **Configuración** > **Seguridad** y active **Orígenes desconocidos**. Si no activa esta opción, aparece el mensaje siguiente al intentar instalar una aplicación: "Instalación bloqueada. Por motivos de seguridad, el dispositivo está configurado para bloquear las instalaciones de aplicaciones procedentes de orígenes desconocidos". Puede pulsar **Configuración** en el mensaje para ir directamente a **Orígenes desconocidos**.  

> [!Note]
> Si su organización usa software de administración de gastos de telecomunicaciones, deberá completar algunos pasos adicionales antes de que el dispositivo esté completamente inscrito. Descubra más [aquí](enroll-your-device-with-telecom-expense-management-android.md).

Si aparece un error al intentar inscribir el dispositivo en Intune, puede [Enviar registros al equipo de soporte técnico de su empresa por correo electrónico](send-logs-to-your-it-admin-by-email-android.md).  

¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  