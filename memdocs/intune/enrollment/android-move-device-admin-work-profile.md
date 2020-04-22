---
title: Traslado de dispositivos Android del administrador de dispositivos a la administración de perfil de trabajo
titleSuffix: Microsoft Intune
description: Traslade dispositivos Android del administrador de dispositivos a la administración de perfil de trabajo en Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f16c39ff0af44918099863be5d23ec9fe564493
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "80624910"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Traslado de dispositivos Android del administrador de dispositivos a la administración de perfil de trabajo

Puede ayudar a los usuarios a trasladar sus dispositivos Android de administrador de dispositivos a la administración de perfil de trabajo mediante el uso de la configuración de cumplimiento para **bloquear dispositivos administrados con el administrador de dispositivos**. Esta opción permite hacer que un dispositivo no sea compatible si se administra con el administrador de dispositivos. 

Cuando los usuarios ven que no cumplen los requisitos por este motivo, pueden pulsar **Resolver**. Se les dirigirá a una lista de comprobación que les guiará por los pasos siguientes:
1. Anulación de la inscripción desde la administración de administradores de dispositivos
2. Inscripción en la administración de perfiles de trabajo
3. Resuelva problemas de cumplimiento. 

## <a name="prerequisites"></a>Requisitos previos

- Los usuarios deben tener [dispositivos inscritos por el administrador de dispositivos Android](android-enroll-device-administrator.md) con el Portal de empresa de Android, versión 5.0.4720.0 o posterior.
- Configure la administración de perfiles de trabajo de Android [conectando su cuenta de inquilino de Intune a su cuenta de Android Enterprise](connect-intune-android-enterprise.md).
- [Establezca la inscripción del perfil de trabajo de Android Enterprise](android-work-profile-enroll.md) para el grupo de usuarios que se está trasladando al perfil de trabajo de Android.
- Considere la posibilidad de aumentar los límites de dispositivos de usuario. Al anular la inscripción de los dispositivos de la administración de los administradores de dispositivos, es posible que los registros de dispositivo no se quiten inmediatamente. Para proporcionar un margen durante este período, puede que necesite aumentar la capacidad del límite de dispositivos para que los usuarios puedan inscribirse en la administración de perfiles de trabajo.
  - [Establezca la configuración del dispositivo Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) para el número máximo de dispositivos por usuario.
  - Ajuste las [restricciones del límite de dispositivos de Intune](enrollment-restrictions-set.md#create-a-device-limit-restriction) estableciendo el límite de dispositivos. 

## <a name="create-device-compliance-policy"></a>Creación de una directiva de cumplimiento de dispositivos

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Dispositivos** > **Directivas de cumplimiento** > **Directivas** > **Crear directiva**.

    ![Creación de directiva](./media/android-move-device-admin-work-profile/create-policy.png)

2. En la página **Crear una directiva**, establezca **Plataforma** en **Administrador de dispositivos de Android** > **Crear**.
3. En la página de los **datos básicos**, escriba un **nombre** y una **descripción** > **Siguiente**.

    ![Página de aspectos básicos](./media/android-move-device-admin-work-profile/basics.png)
    
4. En la página de **configuración de cumplimiento**, en la sección **Estado del dispositivo**, establezca la opción para **bloquear dispositivos administrados con el administrador de dispositivos** en **Sí** > **Siguiente**.

    ![Bloqueo de dispositivos](./media/android-move-device-admin-work-profile/block-devices.png)

5. En la página **Ubicaciones** , puede agregar ubicaciones si lo desea > **Siguiente**.
6. En **Acciones en caso de incumplimiento**, puede establecer la acción **Enviar correo electrónico al usuario final**.

    ![Envío de correo electrónico](./media/android-move-device-admin-work-profile/send-email.png)


    En el correo electrónico, puede incluir la dirección URL siguiente en los mensajes a los usuarios. La dirección URL iniciará el Portal de empresa de Android en la página para **actualizar la configuración del dispositivo**. Esta página inicia su flujo para trasladar a la administración de perfiles de trabajo.
    - `https://portal.manage.microsoft.com/UpdateSettings.aspx`.
    - En el Gobierno de EE. UU., puede usar este vínculo en su lugar: `https://portal.manage.microsoft.us/UpdateSettings.aspx`.
  
    > [!NOTE]
    > - Por supuesto, puede usar hipertexto descriptivo para los vínculos de comunicación con los usuarios. Sin embargo, no use acortadores de URL porque es posible que los vínculos no funcionen si cambian de este modo.
    > - Si el Portal de empresa Android está abierto y en segundo plano, cuando un usuario pulsa el vínculo, es posible que vaya a la última página que tenía abierta.
    > - Los usuarios deben pulsar el vínculo de un dispositivo Android. Si, por el contrario, lo pegan en un explorador, no iniciará el Portal de empresa de Android. 

    Seleccione **Siguiente**.

7. En la página **Etiquetas de ámbito**, seleccione las etiquetas de ámbito que desee incluir.
8. En la página **Asignaciones**, asigne la directiva a un grupo que tenga dispositivos inscritos con la administración del administrador de dispositivos > **Siguiente**.
9. En la página **Revisar y crear**, confirme toda la configuración y, a continuación, seleccione **Crear**.

## <a name="troubleshooting"></a>Solucionar problemas

El [flujo de usuario final para pasar a la nueva configuración de administración de dispositivos](../user-help/move-to-new-device-management-setup.md) guía a los usuarios por la anulación de la inscripción de la administración de administradores de dispositivos y la configuración de la administración de perfiles de trabajo. Los usuarios deben tener [dispositivos inscritos por el administrador de dispositivos Android](android-enroll-device-administrator.md) con el Portal de empresa de Android, versión 5.0.4720.0 o posterior.

### <a name="user-sees-an-error-after-tapping-resolve"></a>El usuario ve un error después de pulsar Resolver.
Si los usuarios ven un error después de pulsar el botón **Resolver**, es probable que se deba a uno de estos motivos:
- La inscripción de perfiles de trabajo no está configurada correctamente (no hay ninguna cuenta de Android Enterprise conectada o las restricciones de inscripción están configuradas para bloquear la inscripción de perfiles de trabajo).
- El dispositivo ejecuta Android 4.4 o anterior, que no admite la inscripción de perfiles de trabajo. 
- El fabricante del dispositivo no admite la inscripción de perfiles de trabajo en el modelo de dispositivo.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>El botón Resolver no aparece en el dispositivo del usuario.
El botón **Resolver** no aparecerá en el dispositivo del usuario si el usuario se inscribe en la administración del administrador de dispositivos después de que se le haya aplicado la directiva de cumplimiento de dispositivos que se explicó anteriormente.

Para que aparezca el botón **Resolver**, el usuario debe posponer la instalación y reiniciar el proceso desde la notificación.

Para evitar esta condición, use restricciones de inscripción para bloquear la inscripción en la administración del administrador de dispositivos.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>El usuario ve un error después de pulsar la dirección URL a la página de actualización de la configuración del dispositivo.
Los usuarios pueden ver una página de error en el explorador al pulsar la dirección URL que lleva la **página de actualización de la configuración del dispositivo** del Portal de empresa de Android. Este error se produce por uno de los siguientes motivos:
- El dispositivo no es un dispositivo Android.
- El dispositivo Android no tiene la aplicación Portal de empresa.
- La versión del Portal de empresa de Android es anterior a 5.0.4720.0.
- El dispositivo Android usa Android 6 o una versión anterior. 

## <a name="next-steps"></a>Pasos siguientes
[Vea el flujo del usuario final](../user-help/move-to-new-device-management-setup.md)
[Administrar dispositivos de perfil de trabajo Android con Intune](android-enterprise-overview.md)
