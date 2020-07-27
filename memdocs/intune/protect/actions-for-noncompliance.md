---
title: 'Acciones y mensajes en caso de incumplimiento con Microsoft Intune: Azure | Microsoft Docs'
description: Cree un correo electrónico de notificación para enviar a los dispositivos no compatibles. Agregue acciones para aplicarlas a los dispositivos que no cumplen las directivas de cumplimiento. Las acciones pueden incluir un período de gracia para cumplir con la directiva, bloquear el acceso a los recursos de red o retirar el dispositivo no compatible.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e5786289e54071d54c11fbb08790e95e54a9377
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461868"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>Configuración de acciones para dispositivos no compatibles en Intune

Para aquellos dispositivos que no cumplen las reglas o las directivas de cumplimiento, puede agregar **Acciones en caso de incumplimiento**. Esta característica configura una secuencia de acciones ordenadas en el tiempo, como enviar un correo al usuario final, entre otras.

## <a name="overview"></a>Introducción

De forma predeterminada, cada directiva de cumplimiento incluye la acción de incumplimiento de **Marcar el dispositivo no compatible** con una programación de cero días (**0**). El resultado de este valor predeterminado es que cuando Intune detecta un dispositivo que no es compatible, lo marca inmediatamente como tal. Una vez que un dispositivo se ha marcado como no compatible, el [Acceso condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) de Azure Active Directory (AD) puede bloquear el dispositivo.

Mediante la configuración de **Acciones en caso de incumplimiento** se obtiene flexibilidad para decidir qué hacer respecto a los dispositivos no compatibles y cuándo hacerlo. Por ejemplo, puede elegir no bloquear el dispositivo inmediatamente y conceder al usuario un período de gracia para convertirlo en compatible.

Para cada acción que establezca, puede configurar una programación que determine cuándo surte efecto la acción. La programación debe indicar el número de días pasados los cuales el dispositivo se marcará como no compatible. También se pueden configurar varias instancias de una acción. Cuando se establecen varias instancias de una acción en una directiva, la acción se ejecutará de nuevo en esa hora programada más tarde en caso de que el dispositivo siga siendo no compatible.

No todas las acciones están disponibles para todas las plataformas.

## <a name="available-actions-for-noncompliance"></a>Acciones disponibles en caso de incumplimiento

A continuación se muestran las acciones disponibles en caso de incumplimiento. A menos que se indique lo contrario, cada acción está disponible para todas las plataformas compatibles con Intune:

- **Marcar dispositivo como no compatible**: de forma predeterminada, esta acción se establece para cada directiva de cumplimiento y tiene una programación de cero (**0**) días, marcando los dispositivos como no compatibles inmediatamente.

  Al cambiar la programación predeterminada, se proporciona un período de gracia en el que un usuario puede corregir incidencias o hacerse compatible sin que se marque como no compatible.

- **Enviar correo electrónico a usuario final**: esta acción envía una notificación por correo electrónico al usuario.
Al habilitar esta acción, se ha de hacer lo siguiente:

  - Seleccione una *plantilla de mensaje de notificación* que envíe esta acción. [Cree una plantilla de mensaje de notificación](#create-a-notification-message-template) para poder asignar una a esta acción. Al crear la notificación personalizada, se personaliza el asunto y el cuerpo del mensaje, y puede incluir el logotipo de la empresa, el nombre de la empresa e información adicional de contacto.
  - Para enviar el mensaje a destinatarios adicionales, seleccione uno o varios de los grupos de Azure AD.

Cuando se envía el correo electrónico, Intune incluye información sobre los dispositivos no compatibles en la notificación de este correo.

- **Bloquear de forma remota el dispositivo no conforme**: use esta acción para emitir un bloqueo remoto de un dispositivo. Después se pide al usuario un PIN o una contraseña para desbloquear el dispositivo. Más información sobre la característica [Bloqueo remoto](../remote-actions/device-remote-lock.md).

  Las siguientes plataformas admiten esta acción:
  - Android:
    - Administrador de dispositivos Android
    - Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado Android
    - Perfil de trabajo de Android Enterprise
    - Dispositivos de quiosco de Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 y versiones posteriores

- **Retirar el dispositivo no compatible**: esta acción quita todos los datos de empresa del dispositivo y quita este de la administración de Intune. Para evitar el borrado accidental de un dispositivo, esta acción admite una programación mínima de **30** días.

  Las siguientes plataformas admiten esta acción:
  - Android:
    - Administrador de dispositivos Android
    - Propietario del dispositivo Android Enterprise
    - Perfil de trabajo de Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 y versiones posteriores

  Más información sobre la [retirada de los dispositivos](../remote-actions/devices-wipe.md#retire).

- **Enviar notificación de inserción al usuario final**: configure esta acción para enviar una notificación de inserción acerca del no cumplimiento de un dispositivo a través de la aplicación Portal de empresa o de la aplicación de Intune en el dispositivo.

  Las siguientes plataformas admiten esta acción:
  - Android:
    - Administrador de dispositivos Android
    - Propietario del dispositivo Android Enterprise
    - Perfil de trabajo de Android Enterprise
  - iOS/iPadOS

  La notificación de inserción se envía la primera vez que un dispositivo se registra con Intune y se detecta que no es compatible con la directiva de cumplimiento. Cuando un usuario selecciona la notificación, se abre la aplicación Portal de empresa o de Intune y muestra información acerca de por qué no son compatibles. Después, el usuario puede tomar medidas para resolver la incidencia. Intune genera la información del mensaje sobre la no compatibilidad y no se puede personalizar.

  > [!IMPORTANT]
  > Intune, la aplicación Portal de empresa y la de Microsoft Intune, no pueden garantizar la entrega de una notificación de inserción. Las notificaciones pueden aparecer después de varias horas de retraso, en caso de que se produzcan. Esto incluye la desactivación de las notificaciones de inserción por parte de los usuarios.
  >
  > No confíe en este método de notificación para mensajes urgentes.

  Cada instancia de la acción envía una notificación una sola vez. Para volver a enviar la misma notificación desde una directiva, configure instancias adicionales de la acción en esa directiva, cada una con una programación distinta.
  
  Por ejemplo, se puede programar la primera acción a los cero días y, después, agregar una segunda instancia de la acción establecida a los tres días. Este retraso antes de la segunda notificación proporciona al usuario unos días para resolver la incidencia y evita la segunda notificación.

  Para evitar el envío de correo no deseado a los usuarios que tengan demasiados mensajes duplicados, revise y optimice las directivas de cumplimiento que incluyan una notificación de inserción de incumplimiento. Revise también las programaciones a fin de evitar que se envíen notificaciones de repetición para la misma incidencia con demasiada frecuencia.

  Tenga en cuenta lo siguiente:
  - En el caso de una sola directiva que incluya varias instancias de un conjunto de notificaciones de inserción para el mismo día, solo se envía una notificación única para ese día.

  - Cuando hay varias directivas de cumplimiento que incluyen las mismas condiciones de cumplimiento y la acción de notificación de inserción con la misma programación, Intune envía varias notificaciones al mismo dispositivo en el mismo día.

## <a name="before-you-begin"></a>Antes de comenzar

Se pueden [agregar acciones en caso de incumplimiento](#add-actions-for-noncompliance) cuando se configure la directiva de cumplimiento de dispositivos o, más adelante, editando la directiva. Se pueden agregar acciones adicionales a cada directiva para satisfacer sus necesidades. Tenga en cuenta que cada directiva de cumplimiento incluye automáticamente la acción predeterminada de incumplimiento que marca los dispositivos como no compatibles, con una programación establecida en cero días.

Para usar las directivas de cumplimiento de dispositivos a fin de bloquear los dispositivos del uso de los recursos corporativos, se debe configurar el acceso condicional de Azure AD. Consulte [¿Qué es el acceso condicional en Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) o [¿Cuáles son las formas habituales de usar el acceso condicional con Intune?](conditional-access-intune-common-ways-use.md) para obtener instrucciones.

A fin de crear una directiva de cumplimiento de dispositivos, vea la guía siguiente específica para plataformas:

- [Android](compliance-policy-create-android.md)
- [Perfiles de trabajo Android](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>Creación de una plantilla de mensaje de notificación

Para enviar correo electrónico a los usuarios, cree una plantilla de mensaje de notificación. Cuando un dispositivo no es compatible, los detalles que especifica en la plantilla se muestran en el correo electrónico enviado a los usuarios.

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Seguridad de punto de conexión** > **Conformidad de dispositivos** > **Notificaciones** > **Crear notificación**.
3. En *Aspectos básicos*, especifique la información siguiente:

   - **Nombre**
   - **Asunto**
   - **Message**

4. También en *Aspectos básicos*, configure las siguientes opciones para la notificación:

   - **Encabezado de correo electrónico: incluir logotipo de la empresa** (valor predeterminado = *Habilitar*): el logotipo que se carga como parte de la personalización de marca del Portal de empresa se usa para las plantillas de correo electrónico. Para más información sobre la personalización de marca del Portal de empresa, vea [Personalización de la marca de empresa](../apps/company-portal-app.md#customizing-the-user-experience).
   - **Pie de página de correo electrónico: incluir nombre de la empresa** (valor predeterminado = *Habilitar*).
   - **Pie de página de correo electrónico: incluir información de contacto** (valor predeterminado = *Habilitar*).
   - **Vínculo del sitio web de Portal de empresa** (valor predeterminado = *Deshabilitar*): cuando se establece en *Habilitar*, el correo electrónico incluye un vínculo al sitio web de Portal de empresa.

   > [!div class="mx-imgBorder"]
   > ![Ejemplo de un mensaje de notificación compatible en Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Seleccione **Siguiente** para continuar.

5. En **Revisar y crear**, revise las configuraciones para asegurarse de que la plantilla de mensaje de notificación está lista para usarse. Seleccione **Crear** para terminar de crear la notificación.

> [!NOTE]
> También puede seleccionar una plantilla de notificación existente creada anteriormente y **Editar** su información para actualizar la plantilla.

## <a name="add-actions-for-noncompliance"></a>Adición de acciones en caso de incumplimiento

Cuando se crea una directiva de cumplimiento de dispositivos, Intune crea automáticamente una acción en caso de incumplimiento. Si un dispositivo no cumple la directiva de cumplimiento, esta acción marca el dispositivo como no conforme. Puede personalizar cuánto tiempo se marca el dispositivo como no conforme. Esta acción no se puede suprimir.

Puede agregar acciones opcionales al crear una directiva de cumplimiento o bien actualizar una directiva existente.

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Directivas de cumplimiento** > **Directivas**, seleccione una de las directivas y, luego, **Propiedades**.

   ¿Aún no tiene una directiva? Cree una directiva de [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) o de otra plataforma.

   > [!NOTE]
   > Los dispositivos JAMF y los dispositivos dirigidos con grupos de dispositivos no pueden recibir acciones de cumplimiento por el momento.

3. Seleccione **Actions for noncompliance** (Acciones en caso no conformidad) > **Agregar**.

4. Seleccione la **Acción**:

   - **Enviar correo electrónico a usuario final**: cuando el dispositivo no sea compatible, elija la opción de enviar un correo al usuario. Además:
     - Elija la **Plantilla de mensaje** que ha creado antes
     - Escriba los **Destinatarios adicionales** mediante la selección de grupos

   - **Bloquear de forma remota el dispositivo no conforme**: cuando el dispositivo no sea compatible, bloquéelo. Esta acción obliga al usuario a escribir un PIN o una contraseña para desbloquear el dispositivo.

   - **Retirar el dispositivo no compatible**: cuando el dispositivo no es compatible, quite todos los datos de empresa del dispositivo y quítelo de la administración de Intune.

   - **Enviar notificación de inserción al usuario final**: configure esta acción para enviar una notificación de inserción acerca del no cumplimiento de un dispositivo a través de la aplicación Portal de empresa o de la aplicación de Intune en el dispositivo.

5. Configurar una **programación**: escriba el número de días (de 0 a 365) después del incumplimiento para desencadenar la acción en los dispositivos de los usuarios. (*Retirar el dispositivo no compatible* admite como mínimo 30 días). Después de este período de gracia, puede aplicar una directiva de [acceso condicional](conditional-access-intune-common-ways-use.md). Si escribe **0** (cero) para el número de días, el acceso condicional surte efecto **inmediatamente**. Por ejemplo, si un dispositivo no es compatible, use el acceso condicional para bloquear el acceso al correo electrónico, SharePoint y otros recursos de la organización inmediatamente.

   Al crear una directiva de cumplimiento, se crea automáticamente la acción **Marcar el dispositivo como no conforme** y se establece también automáticamente en **0** días (inmediatamente). Con esta acción, cuando el dispositivo se registra, se evalúa como no conforme inmediatamente. Si también se usa el acceso condicional, este se inicia inmediatamente. Si desea permitir un período de gracia, cambie la **Programación** en la acción **Marcar el dispositivo como no conforme**.

   En la directiva de cumplimiento, por ejemplo, también desea notificar al usuario. Puede agregar la acción **Enviar correo electrónico a usuario final**. En la acción **Enviar correo electrónico**, debe establecer el valor de **Programación** en dos días. Si el dispositivo o el usuario final se siguen evaluando como no conformes el día 2, su correo electrónico se enviará dicho día. Si quiere volver a enviar al usuario un correo electrónico de incumplimiento el día 5, agregue otra acción y establezca **Programación** en cinco días.

   Para obtener más información sobre el cumplimiento y las acciones integradas, consulte la [información general de cumplimiento](device-compliance-get-started.md).

6. Cuando termine, haga clic en **Agregar** > **Aceptar** para guardar los cambios.

## <a name="next-steps"></a>Pasos siguientes

[Supervise las directivas](compliance-policy-monitor.md).
