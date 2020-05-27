---
title: Cómo solucionar problemas de la implementación de directivas de protección de aplicaciones en Intune
description: Describe cómo solucionar los problemas que puede experimentar al implementar directivas de protección de aplicaciones de Intune.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: troubleshooting
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 8443ca01a0ca1647e8069fdccf1d71aef74c23d8
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989470"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Solución de problemas de la implementación de directivas de protección de aplicaciones en Intune

## <a name="introduction"></a>Introducción

Este artículo le ayuda a comprender y solucionar problemas al aplicar directivas de protección de aplicaciones en Microsoft Intune. Siga los pasos de las secciones que se aplican a su situación.

## <a name="basic-steps"></a>Pasos básicos

### <a name="collect-initial-data"></a>Recopilación inicial de datos

Antes de empezar a solucionar problemas, debe recopile información básica que puede ayudarle a comprender mejor el problema y reducir el tiempo necesario para encontrar una solución.

Recopile la información siguiente:

- ¿Qué configuración de directiva no se ha aplicado? ¿Se ha aplicado alguna directiva?
- ¿Cuál es la experiencia del usuario? ¿Los usuarios han instalado e iniciado la aplicación de destino?
- ¿Cuándo empezó el problema? ¿Ha funcionado alguna vez la protección de aplicaciones?
- ¿Qué plataforma (Android o iOS) presenta el problema?
- ¿Cuántos usuarios están afectados? ¿Se ven afectados todos los dispositivos o solo algunos?
- ¿Cuántos dispositivos se ven afectados? ¿Se ven afectados todos los dispositivos o solo algunos?
- Aunque la directiva de protección de aplicaciones de Intune no requiere un servicio de administración de dispositivos móviles (MDM), ¿los usuarios afectados usan Intune o un servicio EMM de terceros?
- ¿Se ven afectadas todas las aplicaciones administradas o solo algunas? Por ejemplo, ¿se ven afectadas las aplicaciones de línea de negocio con [Intune App SDK](../developer/app-sdk-get-started.md), pero no las aplicaciones de la tienda?

Ya puede empezar a solucionar problemas basándose en las respuestas a estas preguntas.

### <a name="verify-prerequisites"></a>Comprobación de los requisitos previos

El siguiente paso en la solución de problemas consiste en comprobar si se cumplen todos los requisitos previos.

Aunque puede usar directivas de protección de aplicaciones en Intune independientes de soluciones de MDM, deben cumplirse los siguientes requisitos previos:

- El usuario debe tener una licencia de Intune asignada.
- El usuario debe pertenecer a un grupo de seguridad de destino de una directiva de protección de aplicaciones. La misma directiva de protección de aplicaciones debe tener como destino la aplicación específica que se va a usa.
- En el caso de los dispositivos Android, se requiere la aplicación Portal de empresa para recibir directivas de protección de aplicaciones.
- Si usa aplicaciones de [Word, Excel o PowerPoint](https://products.office.com/business/office), deben cumplirse los siguientes requisitos adicionales:
    - El usuario debe tener una licencia de [Aplicaciones de Microsoft 365 para negocios o empresas](https://products.office.com/business/compare-more-office-365-for-business-plans) asignada a su cuenta de Azure Active Directory (Azure AD). La suscripción debe incluir las aplicaciones de Office en dispositivos móviles y puede incluir una cuenta de almacenamiento en la nube con [OneDrive para la Empresa](https://onedrive.live.com/about/business/). Las licencias de Office 365 se pueden asignar en el [centro de administración de Microsoft 365](https://admin.microsoft.com) siguiendo [estas instrucciones](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).
    - El usuario debe tener una ubicación administrada configurada mediante la funcionalidad específica **Guardar como**. Este comando se encuentra en la opción de configuración **Guardar copias de los datos de la organización** de la directiva de protección de aplicaciones. Por ejemplo, si la ubicación administrada es [OneDrive](https://onedrive.live.com/about/), la aplicación de OneDrive debe estar configurada en la aplicación de Word, Excel o PowerPoint del usuario.
    - Si la ubicación administrada es OneDrive, la directiva de protección de aplicaciones implementada para el usuario debe tener como destino la aplicación.

  > [!NOTE]
  > Las aplicaciones móviles de Office actualmente solo admiten SharePoint Online y no SharePoint local.

- Si usa directivas de protección de aplicaciones de Intune junto con recursos locales (Microsoft Skype Empresarial y Microsoft Exchange Server), debe habilitar la [autenticación moderna híbrida (HMA) para Skype Empresarial y Exchange](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

Las directivas de protección de aplicaciones de Intune requieren que la identidad del usuario sea coherente entre la aplicación e [Intune App SDK](../developer/app-sdk-get-started.md). La única manera de garantizar esta coherencia es a través de la autenticación moderna. Hay escenarios en los que las aplicaciones pueden funcionar en una configuración local sin autenticación moderna. Sin embargo, los resultados no son coherentes ni están garantizados.

Para obtener más información acerca de cómo habilitar la HMA para las configuraciones híbridas y locales de Skype Empresarial, consulte los siguientes artículos:

- **Configuración híbrida**<br>
[Disponibilidad general de la autenticación moderna híbrida para Skype Empresarial y Exchange](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **Configuración local**<br>
[Autenticación moderna para Skype Empresarial local con AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>Comprobación del estado de la directiva de protección de aplicaciones

Para comprobar el estado de protección de las aplicaciones, siga estos pasos:

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Aplicaciones** > **Supervisar** > **Estado de protección de la aplicación** y, luego, el icono **Usuarios asignados**.
3. En la página **Informes de aplicaciones**, seleccione **Seleccionar usuario** para abrir una lista de usuarios y grupos.
4. Busque a uno de los usuarios afectados en la lista y, a continuación, haga clic en **Seleccionar usuario**. En la parte superior del panel "Informes de aplicaciones", puede ver si el usuario tiene licencia para la protección de aplicaciones y para O365. También puede ver el estado de la aplicación para todos los dispositivos del usuario.
5. Tome nota de la información importante, como las aplicaciones de destino, los tipos de dispositivos, las directivas, el estado de sincronización de los dispositivos y la hora de la última sincronización.

> [!NOTE]
> Las directivas de protección de aplicaciones solo se aplican cuando se usan aplicaciones en el ámbito profesional. Por ejemplo, cuando el usuario accede a las aplicaciones con una cuenta profesional.

Para obtener más información, consulte el artículo [Validación de la configuración de la directiva de protección de aplicaciones en Microsoft Intune](../apps/app-protection-policies-validate.md).

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Comprobación de la coherencia de la identidad del usuario entre la aplicación e Intune App SDK

En la mayoría de los escenarios, los usuarios inician sesión en sus cuentas mediante su nombre principal de usuario (UPN). Sin embargo, en algunos entornos (como los escenarios locales), los usuarios pueden usar otro tipo de credenciales de inicio de sesión. En estos casos, podría encontrar que el UPN que se usa en la aplicación no coincide con el UPN usado en Azure AD. Cuando pasa esto, las directivas de protección de aplicaciones no se aplican del modo esperado.

El procedimiento recomendado de Microsoft es hacer coincidir el UPN con la dirección SMTP principal. Este procedimiento permite a los usuarios iniciar sesión en aplicaciones administradas, la protección de aplicaciones de Intune y otros recursos de Azure AD con una identidad coherente. Para obtener más información, vea el artículo [Rellenado de userPrincipalName de Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Si su entorno requiere métodos de inicio de sesión alternativos, consulte el artículo [Configuración de un identificador de inicio de sesión alternativo](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), en concreto la sección [Autenticación moderna híbrida con un identificador alternativo](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Comprobación de que el usuario es el destinatario

Las directivas de protección de aplicaciones de Intune deben estar dirigidas a usuarios. Si no asigna una directiva de protección de aplicaciones a un usuario o grupo de usuarios, esta no se aplicará.

Para comprobar que la directiva se aplica al usuario de destino, siga estos pasos:

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Aplicaciones** > **Supervisar** > **Estado de protección de la aplicación** y, a continuación, seleccione el icono **Estado del usuario** (según la plataforma del sistema operativo del dispositivo).
En el panel **Informes de aplicaciones** que se abre, elija **Seleccionar usuario** para buscar un usuario.
3. Seleccione el usuario de la lista. Puede ver los detalles de ese usuario.

Cuando asigne la directiva a un grupo de usuarios, asegúrese de que el usuario esté en ese grupo. Para ello, siga estos pasos:

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Grupos > Todos los grupos** y, a continuación, busque y seleccione el grupo que se usa para la asignación de la directiva de protección de aplicaciones.
3. En la sección **Administrar**, seleccione **Miembros**.
4. Si el usuario afectado no aparece en la lista, revise el artículo [Administración del acceso a recursos y aplicaciones con grupos en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) y sus reglas de pertenencia a grupos. Asegúrese de que el usuario afectado está incluido en el grupo.
5. Asegúrese de que el usuario afectado no está en ninguno de los grupos excluidos de la directiva.

> [!IMPORTANT]
> - La directiva de protección de aplicaciones de Intune debe estar asignada a grupos de usuarios, no a grupos de dispositivos.
> - Si el dispositivo afectado usa el Programa de inscripción de dispositivos (DEP) de Apple, asegúrese de que la **afinidad de usuario** está habilitada. La afinidad de usuario es necesaria para todas las aplicaciones que requieran la autenticación de usuario en DEP.
> - Si el dispositivo afectado usa Android Enterprise, solo los perfiles de trabajo admitirán las directivas de protección de aplicaciones.


### <a name="verify-that-the-managed-app-is-targeted"></a>Comprobación de que la aplicación administrada es el destino

Al configurar directivas de protección de aplicaciones de Intune, las aplicaciones de destino deben usar [Intune App SDK](../developer/app-sdk-get-started.md). De lo contrario, es posible que las directivas de protección de aplicaciones no funcionen correctamente.

Asegúrese de que la aplicación de destino aparece entre las [aplicaciones protegidas de Microsoft Intune](../apps/apps-supported-intune-apps.md). En el caso de las aplicaciones de línea de negocio o personalizadas, compruebe que las aplicaciones usan la versión más reciente de [Intune App SDK](../developer/app-sdk-get-started.md). Tenga en cuenta lo siguiente:

En el caso de iOS, este procedimiento es importante porque cada versión contiene correcciones que afectan al modo en que se aplican estas directivas y a cómo funcionan. Para obtener más información, vea las [versiones para iOS de Intune App SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
En el caso de Android, este procedimiento no es tan importante. Sin embargo, los usuarios deben tener instalada la versión más reciente de la aplicación Portal de empresa porque esta aplicación funciona como agente de directivas.

> [!NOTE]
> A partir de septiembre de 2019, Intune pasará a admitir aplicaciones de iOS que tienen Intune App SDK 8.1.1 y versiones posteriores. Ya no se admitirán las aplicaciones compiladas con versiones del SDK anteriores a 8.1.1. 

## <a name="more-information"></a>Más información

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Requisitos especiales para dispositivos administrados por MDM de Intune

Al crear una directiva de protección de aplicaciones, puede dirigirla a todos los tipos de aplicaciones o a los siguientes tipos:

- Aplicaciones en dispositivos no administrados
- Aplicaciones en dispositivos administrados por Intune
- Aplicaciones en el perfil de trabajo de Android

> [!NOTE] 
> Para especificar los tipos de aplicaciones, establezca **Destinar a todos los tipos de aplicaciones** en **No** y, a continuación, seleccione los tipos que quiera en la lista **Tipos de aplicaciones**.

En el caso de iOS, se requieren los siguientes ajustes adicionales en la [configuración de la aplicación](../apps/app-configuration-policies-use-ios.md) para dirigir la configuración de la directiva de protección de aplicaciones a las aplicaciones de dispositivos inscritos en Intune:

- **IntuneMAMUPN** debe configurarse para todas las aplicaciones administradas por MDM (de Intune o de un servicio EMM de terceros). Para obtener más información, consulte la sección "Configurar el valor de UPN de usuario para Microsoft Intune o para una solución EMM de terceros".
- **IntuneMAMDeviceID** debe configurarse para todas las aplicaciones administradas por MDM de línea de negocio y de terceros.
- **IntuneMAMDeviceID** debe configurarse como el token de identidad del dispositivo. Por ejemplo, clave = IntuneMAMDeviceID, valor = {{deviceID}}. Para obtener más información, vea [Agregar directivas de configuración de aplicaciones para dispositivos iOS administrados](../apps/app-configuration-policies-use-ios.md).
- Si solo está configurado el valor de **IntuneMAMDeviceID**, la directiva de protección de aplicaciones de Intune considerará el dispositivo como no administrado.

### <a name="scenario-policy-changes-are-not-working"></a>Escenario: Los cambios en la directiva no funcionan
[Intune App SDK](../developer/app-sdk-get-started.md) comprueba con regularidad si hay cambios en la directiva. Sin embargo, este proceso se puede retrasar por cualquiera de los siguientes motivos:

- La aplicación no se ha sincronizado con el servicio.
- Se ha quitado la aplicación Portal de empresa del dispositivo.

La directiva de protección de aplicaciones de Intune se basa en la identidad del usuario. Por lo tanto, se requiere un inicio de sesión válido en la aplicación mediante una cuenta profesional o educativa y una conexión estable con el servicio. Si el usuario no ha iniciado sesión en la aplicación o la aplicación Portal de empresa se ha quitado del dispositivo, no se aplicarán las actualizaciones de las directivas.

Asimismo, los cambios y las actualizaciones en la directiva de protección de aplicaciones pueden tardar hasta ocho horas en aplicarse. Si es necesario, el cierre de todas las aplicaciones y el reinicio del dispositivo normalmente obliga a que la actualización de la directiva se aplique antes.

Para comprobar el estado de protección de las aplicaciones, siga estos pasos:

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Aplicaciones** > **Supervisar** > **Estado de protección de la aplicación** y, luego, el icono **Usuarios asignados**.
3. En la página "Informes de aplicaciones", haga clic en **Seleccionar usuario** para abrir una lista de usuarios y grupos.
4. Busque a uno de los usuarios afectados en la lista y, a continuación, haga clic en **Seleccionar usuario**.
5. Revise las directivas que se aplican actualmente, incluido su estado y la hora de la última sincronización.
6. Si el estado es **No protegido** o la pantalla indica que no ha habido una sincronización reciente, compruebe si el usuario tiene una conexión de red estable. En el caso de los usuarios de Android, asegúrese de que tienen instalada la versión más reciente de la aplicación Portal de empresa.

> [!IMPORTANT]
> [Intune App SDK](../developer/app-sdk-get-started.md) comprueba el borrado selectivo cada 30 minutos. Sin embargo, es posible que los cambios en la directiva existente para los usuarios que ya han iniciado sesión no aparezcan hasta ocho horas más tarde. Para acelerar este proceso, indique al usuario que cierre sesión en la aplicación y que vuelva a iniciar sesión o a reiniciar su dispositivo.

La directiva de protección de aplicaciones de Intune incluye compatibilidad con varias identidades. Intune puede aplicar directivas de protección de aplicaciones solo a la cuenta profesional o educativa con la que se ha iniciado sesión en la aplicación. Sin embargo, solo se admite una cuenta profesional o educativa por dispositivo.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Escenario: Se aplica la directiva, pero los usuarios de iOS todavía pueden transferir archivos de trabajo a aplicaciones no administradas
La característica de **administración Open In** (![botón "Open In"](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg)) para dispositivos iOS puede limitar las transferencias de archivos para que solo se realicen entre las aplicaciones que se implementan en los dispositivos mediante el canal de administración de dispositivos móviles (MDM). Es posible que el usuario pueda transferir archivos de trabajo desde ubicaciones administradas, como OneDrive y Exchange, a aplicaciones o ubicaciones no administradas en función de la configuración. La característica de **administración Open In** de iOS funciona fuera de otros métodos de transferencia de datos. Por lo tanto, no se ve afectado por la configuración de las opciones de **guardar como** y **copiar y pegar**.

Puede usar directivas de protección de aplicaciones de Intune con la característica de **administración Open In** de iOS para proteger los datos de la empresa de las siguientes formas:

- **Dispositivos propiedad de los empleados que no están administrados por una solución de MDM**: puede establecer la configuración de directivas de protección de aplicaciones en **Allow app to transfer data to only managed apps** (Permitir a la aplicación transferir datos solo a aplicaciones administradas por directivas). Si se configura de esta manera, el comportamiento **Open In** en una aplicación administrada por directivas solo proporciona otras aplicaciones administradas por directivas como opción para el uso compartido. Por ejemplo, si un usuario intenta enviar un archivo protegido como datos adjuntos desde OneDrive en la aplicación de correo nativa, el archivo será ilegible.

- **Dispositivos administrados por soluciones de MDM**: en el caso de los dispositivos inscritos en las soluciones de MDM de Intune o de terceros, el uso compartido de datos entre las aplicaciones con directivas de protección de aplicaciones y otras aplicaciones iOS administradas que se implementan mediante MDM está controlado por las directivas de protección de aplicaciones de Intune y por la característica de **administración Open in** de iOS.<br/><br/>
Para asegurarse de que las aplicaciones que implementa mediante una solución de MDM también están asociadas a las directivas de protección de aplicaciones de Intune, configure el valor de UPN de usuario como se describe en [esta sección](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).<br/><br/>Para especificar cómo quiere permitir la transferencia de datos a otras aplicaciones, habilite **Enviar datos de la organización a otras aplicaciones** y seleccione el nivel de uso compartido que prefiera.<br/><br/>Para especificar cómo quiere permitir que una aplicación reciba datos de otras aplicaciones, habilite **Recibir datos de otras aplicaciones** y seleccione el nivel de recepción de datos que prefiera.

Para obtener más información sobre cómo recibir y compartir datos de la aplicación, vea la [configuración de la reubicación de datos](../apps/app-protection-policy-settings-ios.md#data-protection).

Para más información, vea [Administración de transferencias de datos entre aplicaciones iOS en Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md).

## <a name="references"></a>Referencias

Si todavía busca una solución para un problema relacionado, o bien quiere obtener más información sobre Intune, publique una pregunta en nuestro [foro de Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Muchos ingenieros de soporte técnico, MVP y miembros de nuestro equipo de desarrollo visitan los foros. Por lo tanto, es muy probable que encuentre a alguien que tenga la información que necesita.

Para abrir una solicitud de soporte técnico para el equipo de soporte de Microsoft Intune, vea [Cómo obtener asistencia para Microsoft Intune](../fundamentals/get-support.md).

Para obtener más información sobre la directiva de protección de aplicaciones de Intune, consulte los siguientes artículos:

- [Solucionar problemas de la administración de aplicaciones móviles](../apps/troubleshoot-mam.md)
- [Preguntas más frecuentes sobre MAM y la protección de la aplicación](../apps/mam-faq.md)
- [Sugerencia de soporte: Solución de problemas de la directiva de protección de aplicaciones de Intune mediante archivos de registro en dispositivos locales](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

Para obtener las noticias, la información y los consejos técnicos más recientes, consulte nuestros blogs oficiales:

- [Blog del equipo de soporte técnico de Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Blog de Microsoft Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información adicional sobre la solución de problemas de Intune, consulte [Uso del portal de solución de problemas para ayudar a los usuarios de su empresa](../fundamentals/help-desk-operators.md). 
- Obtenga información sobre los problemas conocidos de Microsoft Intune. Para obtener más información, vea [Éxito de clientes de Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- ¿Necesita más ayuda? Consulte [Cómo obtener asistencia para Microsoft Intune](../fundamentals/get-support.md).
