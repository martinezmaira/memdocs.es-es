---
title: Inscripción de un dispositivo Mac con Portal de empresa de Intune | Microsoft Docs
description: Obtenga información sobre cómo inscribir un dispositivo Mac en Intune con la aplicación Portal de empresa.
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/16/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2ef7951217b0b6df21a86ca29a8637385aa65715
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "79337023"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Inscripción de un dispositivo macOS con Portal de empresa  

Inscriba un dispositivo macOS con la aplicación Portal de empresa de Intune para obtener acceso seguro a las aplicaciones, los archivos y la dirección de correo electrónico profesional o educativa de su organización.

Las organizaciones suelen requerir a los usuarios que inscriban sus dispositivos antes de poder acceder a datos confidenciales. Después de haber inscrito el dispositivo, se convierte en *administrado*. La organización puede asignar directivas y aplicaciones al dispositivo mediante un proveedor de administración de dispositivos móviles (MDM), como Intune. Para obtener acceso continuo a la información profesional o educativa del dispositivo, debe configurarlo para que coincida con la configuración de directiva de su organización.  

En este artículo se describe cómo usar la aplicación Portal de empresa para que macOS inscriba, configure y mantenga su dispositivo para que cumpla los requisitos de su organización.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Qué esperar de la aplicación Portal de empresa

Durante la instalación inicial, la aplicación Portal de empresa requiere que inicie sesión y se autentique con su organización. Portal de empresa le informa de cualquier configuración de dispositivo que haya que configurar para satisfacer los requisitos de su organización. Por ejemplo, las organizaciones suelen definir requisitos de caracteres mínimos o máximos para las contraseñas que tendrá que cumplir.    

Después de inscribir el dispositivo, Portal de empresa siempre se asegurará de que el dispositivo esté protegido según los requisitos de su organización. Por ejemplo, si instala una aplicación desde un origen que no es de confianza, Portal de empresa le avisará y podría restringir el acceso a los recursos de su organización. Las directivas de protección de aplicaciones como esta son bastante habituales. Para recuperar el acceso, es probable que deba desinstalar la aplicación que no es de confianza. 

Si después de la inscripción, la organización exige un nuevo requisito de seguridad, como la autenticación multifactor, Portal de empresa se lo notificará. Tendrá la oportunidad de ajustar la configuración para poder seguir trabajando desde su dispositivo.  

Para obtener más información sobre la inscripción, vea [¿Qué ocurre si instalo la aplicación de Portal de empresa e inscribo el dispositivo?](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md).  

## <a name="get-your-macos-device-managed"></a>Conversión del dispositivo macOS en administrado  
Realice los siguientes pasos para inscribir un dispositivo macOS en su organización. Dicho dispositivo debe ejecutar macOS 10.12 o posterior.   

> [!NOTE]
> A lo largo de este proceso, es posible que se le pida permitir que Portal de empresa use la información confidencial que hay almacenada en la cadena de claves. Estos mensajes forman parte de la seguridad de Apple. Cuando reciba el mensaje, escriba la contraseña de la cadena de claves de inicio de sesión y seleccione **Permitir siempre**. Si presiona las teclas **Entrar** o **Retroceso** en el teclado, en vez de eso se seleccionará **Permitir** en el mensaje, lo que puede dar pie a que aparezcan más mensajes.  

### <a name="install-company-portal-app"></a>Instalar la aplicación Portal de empresa  
1. Vaya a [Inscribir mi Mac](https://go.microsoft.com/fwlink/?linkid=853070).  
2. Se descargará el archivo .pkg del instalador de Portal de empresa. Abra el instalador y siga los pasos que aparecen. 
3. Acepte el contrato de licencia de software. 
4. Escriba la contraseña del dispositivo o la huella digital registrada para instalar el software.  
5. Abra Portal de empresa. 

> [!IMPORTANT]
> Puede que Microsoft AutoUpdate se abra para actualizar el software de Microsoft. Una vez instaladas todas las actualizaciones, abra la aplicación Portal de empresa. Para obtener la mejor experiencia de instalación, instale las versiones más recientes de Microsoft AutoUpdate y Portal de empresa.  


### <a name="enroll-your-mac"></a>Inscripción de su dispositivo Mac  


1. Inicie sesión en el Portal de empresa con su cuenta profesional o educativa.  
2. Cuando la aplicación se abra, seleccione **Comenzar**.  
3. Revise lo que su organización puede y no puede ver en el dispositivo inscrito. Luego, seleccione **Continue** (Continuar).
4.  Si se le solicita, escriba la contraseña del dispositivo en la pantalla **Install management profile** (Instalar perfil de administración).

    ![Captura de pantalla de ejemplo de la pantalla Install management profile (Instalar perfil de administración) de Portal de empresa](./media/install-management-profile-macos-1912.PNG)   
5. En la pantalla **Confirmar la administración de dispositivos**, seleccione **Preferencias de sistema abierto**.  

    ![Captura de pantalla de ejemplo de la pantalla Confirmar la administración de dispositivos con el botón "Preferencias de sistema abierto" resaltado](./media/confirm-device-management-macos-1912.PNG)  
6. Se abrirán las preferencias de sistema del dispositivo. Seleccione **Management Profile** (Perfil de administración) en la lista perfiles de dispositivo y, después, **Aprobar** > **Aprobar**.  
    ![Captura de pantalla de ejemplo la pantalla Management Profile (Perfil de administración) de las preferencias del sistema con el botón "Aprobar" resaltado](./media/management-profile-approve-macos-1912.PNG)   
1. Vuelva a Portal de empresa y seleccione **Continuar**.    
2. Es posible que su organización requiera que actualice la configuración del dispositivo. Cuando haya terminado de actualizar la configuración, seleccione **Comprobar configuración**.  

    ![Captura de pantalla de ejemplo la pantalla Actualizar configuración del dispositivo de Portal de empresa con el botón Comprobar configuración resaltado](./media/update-settings-mac-1911.PNG)  
9. Una vez finalizada la instalación, seleccione **Listo**.  


 ## <a name="troubleshooting-and-feedback"></a>Solución de problemas y comentarios   

Si surgen problemas durante la inscripción, vaya a **Ayuda** > **Enviar informe de diagnóstico** para informar del problema a los desarrolladores de aplicaciones de Microsoft. Esta información les ayudará a mejorar la aplicación. También la usarán para tratar de resolver el problema si su personal de TI se pone en contacto con ellos para obtener ayuda.  

Después de informar del problema a Microsoft, puede enviar detalles de su experiencia al personal de soporte técnico de TI. Seleccione **Enviar detalles por correo electrónico**. Indique cuál ha sido su experiencia en el cuerpo del mensaje de correo electrónico. Para encontrar la dirección de correo electrónico del personal de soporte técnico, vaya a la aplicación Portal de empresa > **Contacto**. O bien compruebe el [sitio web Portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  
 

Aparte de esto, el equipo de Portal de empresa de Microsoft Intune estará encantado de recibir sus comentarios. Vaya a **Ayuda** > **Enviar comentarios** para compartir sus opiniones e ideas.  

## <a name="unverified-profiles"></a>Perfiles sin comprobar  
Cuando se consultan los perfiles de administración de dispositivos móviles (MDM) instalados en **Preferencias del sistema** > **Perfiles**, algunos perfiles podrían mostrar un estado Sin comprobar. Mientras el perfil de administración muestre un estado Comprobado, no tiene por qué preocuparse.  

El perfil de administración es lo que define la conexión del canal de MDM. Mientras se compruebe el perfil de administración, cualquier otro perfil entregado a la máquina a través de ese canal, hereda las características de seguridad del perfil de administración.  

## <a name="updating-the-company-portal-app"></a>Actualización de la aplicación del Portal de empresa

La actualización de la aplicación del Portal de empresa se realiza del mismo modo que la de cualquier otra aplicación de Office, a través de Microsoft AutoUpdate para macOS. Obtenga más información sobre cómo [actualizar aplicaciones de Microsoft para macOS](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1).  

## <a name="next-steps"></a>Pasos siguientes  
¿Aún necesita ayuda? Póngase en contacto con el departamento de soporte técnico de la empresa. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  


