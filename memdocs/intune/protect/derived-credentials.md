---
title: Uso de credenciales derivadas para dispositivos móviles en Microsoft Intune - Azure | Microsoft Docs
description: Use credenciales derivadas en dispositivos móviles como método de autenticación para la VPN de Intune, correo electrónico, perfiles de Wi-Fi, aplicaciones, S/MIME y cifrado. Las credenciales derivadas son una implementación de las directrices NIST para la publicación especial 800-157.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e8d4b866ca2086ae11efa10f1967b08f12e55919
ms.sourcegitcommit: d1c7548b4177d720065b822356f9a08d1e1657c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82881033"
---
# <a name="use-derived-credentials-in-microsoft-intune"></a>Uso de credenciales derivadas en Microsoft Intune

*Este artículo se aplica a iOS/iPadOS y dispositivos Android Enterprise totalmente administrados que ejecutan la versión 7.0 y versiones posteriores*.

En un entorno en el que se necesitan tarjetas inteligentes para la autenticación o el cifrado y la firma, ahora puede usar Intune para aprovisionar dispositivos móviles con un certificado que se derive de la tarjeta inteligente de un usuario. Ese certificado se denomina *credencial derivada*. Intune [admite varios emisores de credenciales derivadas](#supported-issuers), aunque solo se puede usar un emisor por inquilino a la vez.

Las credenciales derivadas son una implementación de las directrices del National Institute of Standards and Technology (NIST) para las credenciales derivadas de verificación de identidad personal (PIV) como parte de la publicación especial (SP) 800-157.

**Con la implementación de Intune**:

- El administrador de Intune configura su inquilino para que funcione con un emisor de credenciales derivadas compatible. No es necesario aplicar ninguna configuración específica de Intune en el sistema del emisor de credenciales derivadas.
- El administrador de Intune especifica la **credencial derivada** como *método de autenticación* de los siguientes objetos:
  
  **Para iOS/iPadOS**:
  - Tipos de perfiles comunes, como Wi-Fi, VPN y correo electrónico, que incluye la aplicación de correo electrónico nativa de iOS/iPadOS
  - Autenticación de aplicaciones
  - Firma S/MIME y cifrado

  **Para dispositivos Android Enterprise totalmente administrados**:
  - Tipos de perfiles comunes, como Wi-Fi y VPN
  - Autenticación de aplicaciones
  
- Los usuarios obtienen una credencial derivada usando su tarjeta inteligente en un equipo para autenticarse en el emisor de las credenciales derivadas. Luego, el emisor emite al dispositivo móvil un certificado que se deriva de su tarjeta inteligente.
- Una vez que el dispositivo ha recibido la credencial derivada, se usa para la autenticación, así como para la firma S/MIME y el cifrado, cuando las aplicaciones o los recursos obtienen acceso a perfiles que requieren la credencial derivada.

## <a name="prerequisites"></a>Requisitos previos

Revise la siguiente información antes de configurar su inquilino para usar las credenciales derivadas.

### <a name="supported-platforms"></a>Plataformas compatibles

Intune admite credenciales derivadas en las siguientes plataformas:

- iOS/iPadOS
- Android Enterprise: dispositivos totalmente administrados (versión 7.0 y posteriores)

### <a name="supported-issuers"></a>Emisores admitidos

Intune admite un solo emisor de credenciales derivadas por inquilino. Puede configurar Intune para que funcione con los siguientes emisores:

- **DISA Purebred** (solo iOS): https:\//cyber.mil/pki-pke/purebred/
- **Entrust Datacard**: https://www.entrustdatacard.com/
- **Intercede**: https://www.intercede.com/

Para obtener información importante sobre el uso de los distintos emisores, consulte la guía del emisor en cuestión. Para obtener más información, vea [Planear las credenciales derivadas](#plan-for-derived-credentials) en este artículo.

> [!IMPORTANT]
> Si elimina de su inquilino un emisor de credenciales derivadas, las credenciales derivadas que se hayan configurado con ese emisor dejarán de funcionar.
>
> Consulte [Cambiar el emisor de las credenciales derivadas](#change-the-derived-credential-issuer) más adelante en este artículo.

### <a name="company-portal-app"></a>Aplicación de portal de empresa

Planee la implementación de la aplicación Portal de empresa de Intune en los dispositivos que se van a inscribir en una credencial derivada. Los usuarios de dispositivos usan la aplicación Portal de empresa para iniciar el proceso de inscripción de credenciales.

- Para los dispositivos iOS, consulte [Adición de aplicaciones de la tienda iOS a Microsoft Intune](../apps/store-apps-ios.md).
- Para los dispositivos Android, vea [Adición de aplicaciones de la Tienda Android a Microsoft Intune](../apps/store-apps-android.md).

## <a name="plan-for-derived-credentials"></a>Planear las credenciales derivadas

Tenga presentes las siguientes consideraciones antes de configurar un emisor de credenciales derivadas.

### <a name="1-review-the-documentation-for-your-chosen-derived-credential-issuer"></a>1) Revisar la documentación del emisor de credenciales derivadas elegido

Antes de configurar un emisor, revise la documentación correspondiente para comprender cómo suministra su sistema las credenciales derivadas a los dispositivos.

En función del emisor que elija, puede que necesite personal que esté disponible en el momento de la inscripción para que los usuarios puedan llevar a cabo el proceso. Revise también las configuraciones actuales de Intune a fin de garantizar que no bloquean el acceso necesario para que los dispositivos o los usuarios lleven a cabo la solicitud de credenciales.

Por ejemplo, puede usar el acceso condicional para bloquear el acceso al correo electrónico en los dispositivos no compatibles. Si confía en las notificaciones por correo electrónico para informar al usuario de que debe iniciar el proceso de inscripción de credenciales derivadas, es posible que los usuarios no reciban esas instrucciones hasta que cumplan la directiva.

Del mismo modo, algunos flujos de trabajo de solicitud de credenciales derivadas requieren el uso de la cámara del dispositivo para escanear un código QR que aparece en pantalla. Este código vincula ese dispositivo a la solicitud de autenticación que se efectuó en el emisor de credenciales derivadas con las credenciales de la tarjeta inteligente del usuario. Si las directivas de configuración del dispositivo bloquean el uso de la cámara, el usuario no podrá llevar a cabo la solicitud de inscripción de credenciales derivadas.

**Información general**:

- Solo puede configurar un emisor por inquilino a la vez; ese emisor está disponible para todos los usuarios y los dispositivos compatibles en el inquilino.

- No se notificará a los usuarios de que deben inscribirse en las credenciales derivadas hasta que les aplique una directiva que requiera credenciales derivadas.

- La notificación puede realizarse a través de una notificación de la aplicación del Portal de empresa, por correo electrónico o ambos. Si decide usar notificaciones por correo electrónico y habilita el acceso condicional, es posible que los usuarios no reciban la notificación por correo electrónico si su dispositivo no es compatible.

### <a name="2-review-the-end-user-workflow-for-your-chosen-issuer"></a>2) Revisar el flujo de trabajo del usuario final del emisor elegido

A continuación se indican las consideraciones clave de cada asociado admitido.  Familiarícese con esta información para asegurarse de que las directivas y configuraciones de Intune no impidan que los usuarios y los dispositivos lleven a cabo correctamente la inscripción de una credencial derivada de ese emisor.

#### <a name="disa-purebred"></a>DISA Purebred

Revise el flujo de trabajo del usuario específico de la plataforma para los dispositivos que se van a usar con las credenciales derivadas.

- [iOS e iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-disa-purebred)

**Los requisitos clave incluyen lo siguiente**:

- Los usuarios necesitan tener acceso a un equipo o a un quiosco en el que puedan usar su tarjeta inteligente para autenticarse en el emisor.
- Los dispositivos que se inscriban en una credencial derivada deben instalar la aplicación Portal de empresa de Intune.
- Use Intune para [implementar la aplicación DISA Purebred](#deploy-the-disa-purebred-app) en los dispositivos que se van a inscribir en una credencial derivada. Esta aplicación se debe implementar mediante Intune para que se administre y pueda funcionar después con la aplicación del Portal de empresa de Intune. Esta aplicación la usan los usuarios del dispositivo para llevar a cabo la solicitud de credenciales derivadas.
- La aplicación DISA Purebred requiere una [VPN por aplicación](../configuration/vpn-settings-configure.md) para garantizar que la aplicación pueda acceder a DISA Purebred durante la inscripción de la credencial derivada.
- Los usuarios del dispositivo deben trabajar con un agente activo durante el proceso de inscripción. Durante la inscripción se proporciona al usuario códigos de acceso de un solo uso y de tiempo limitado a medida que avanza en el proceso de inscripción.
- Cuando se realizan cambios en una directiva que usa credenciales derivadas, como la creación de un nuevo perfil de Wi-Fi, se notifica a los usuarios de iOS e iPadOS que abran la aplicación Portal de empresa.
- Se notifica a los usuarios que abran la aplicación Portal de empresa cuando necesiten renovar sus credenciales derivadas.

Para obtener información sobre cómo obtener y configurar la aplicación DISA Purebred, vea [Implementar la aplicación DISA Purebred](#deploy-the-disa-purebred-app) más adelante en este artículo.

#### <a name="entrust-datacard"></a>Entrust Datacard

Revise el flujo de trabajo del usuario específico de la plataforma para los dispositivos que se van a usar con las credenciales derivadas.

- [iOS e iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-entrust-datacard)
- [Dispositivos Android Enterprise totalmente administrados](../user-help/enroll-android-device-entrust-datacard.md)

**Los requisitos clave incluyen lo siguiente**:

- Los usuarios necesitan tener acceso a un equipo o a un quiosco en el que puedan usar su tarjeta inteligente para autenticarse en el emisor.
- Los dispositivos que se inscriban en una credencial derivada deben instalar la aplicación Portal de empresa de Intune.
- Uso de una cámara de dispositivo para escanear un código QR que vincule la solicitud de autenticación a la solicitud de la credencial derivada desde el dispositivo móvil.
- A través de la aplicación Portal de empresa o del correo electrónico se solicita a los usuarios que se inscriban en las credenciales derivadas.
- Cuando se realizan cambios en una directiva que usa credenciales derivadas, como la creación de un nuevo perfil de Wi-Fi:
  - **iOS y iPadOS**: se notifica a los usuarios que abran la aplicación Portal de empresa.
  - **Dispositivos Android Enterprise totalmente administrados**: no es necesario abrir la aplicación Portal de empresa.
- Se notifica a los usuarios que abran la aplicación Portal de empresa cuando necesiten renovar sus credenciales derivadas.

#### <a name="intercede"></a>Intercede

Revise el flujo de trabajo del usuario específico de la plataforma para los dispositivos que se van a usar con las credenciales derivadas.

- [iOS e iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-intercede)
- [Dispositivos Android Enterprise totalmente administrados](../user-help/enroll-android-device-intercede.md)

**Los requisitos clave incluyen lo siguiente**:

- Los usuarios necesitan tener acceso a un equipo o a un quiosco en el que puedan usar su tarjeta inteligente para autenticarse en el emisor.
- Los dispositivos que se inscriban en una credencial derivada deben instalar la aplicación Portal de empresa de Intune.
- Uso de una cámara de dispositivo para escanear un código QR que vincule la solicitud de autenticación a la solicitud de la credencial derivada desde el dispositivo móvil.
- A través de la aplicación Portal de empresa o del correo electrónico se solicita a los usuarios que se inscriban en las credenciales derivadas.
- Cuando se realizan cambios en una directiva que usa credenciales derivadas, como la creación de un nuevo perfil de Wi-Fi:
  - **iOS y iPadOS**: se notifica a los usuarios que abran la aplicación Portal de empresa.
  - **Dispositivos Android Enterprise totalmente administrados**: no es necesario abrir la aplicación Portal de empresa.
- Se notifica a los usuarios que abran la aplicación Portal de empresa cuando necesiten renovar sus credenciales derivadas.

### <a name="3-deploy-a-trusted-root-certificate-to-devices"></a>3) Implementar un certificado raíz de confianza en los dispositivos

Se usa un certificado raíz de confianza con credenciales derivadas para comprobar que la cadena de certificados de las credenciales derivadas es válida y de confianza. Incluso si no se hace referencia directa a él mediante una directiva, se requiere un certificado raíz de confianza. Vea [Configuración de un perfil de certificado para sus dispositivos en Microsoft Intune](certificates-configure.md).

### <a name="4-provide-end-user-instructions-for-how-to-get-the-derived-credential"></a>4) Proporcionar instrucciones al usuario final sobre cómo obtener la credencial derivada

Cree y proporcione orientación a sus usuarios sobre cómo iniciar el proceso de inscripción de credenciales derivadas y dirigirlos al flujo de trabajo de inscripción de credenciales derivadas para el emisor elegido.

Le recomendamos que proporcione una dirección URL que hospede su guía. Esta dirección URL se especifica al configurar el emisor de credenciales derivadas de su inquilino y se pone a disposición desde la aplicación Portal de empresa. Si no especifica su propia dirección URL, Intune proporcionará un vínculo a los detalles genéricos. Esta información detallada no puede cubrir todos los escenarios y es posible que no sea precisa para su entorno.

### <a name="dive-idsupported-objects-5-deploy-intune-policies-that-require-derived-credentials"></a><dive id="supported-objects"> 5) Implementación de directivas de Intune que requieran credenciales derivadas

Cree directivas o edite las directivas existentes para usar las credenciales derivadas. Las credenciales derivadas reemplazan a otros métodos de autenticación para los objetos siguientes:

- Autenticación de aplicaciones
- Wi-Fi
- VPN
- Correo electrónico (solo iOS)
- Firma S/MIME y cifrado, incluido Outlook (solo iOS)

Evite exigir el uso de una credencial derivada para acceder a un proceso que se usará como parte del proceso para obtener la credencial derivada, ya que puede impedir que los usuarios lleven a cabo la solicitud.

## <a name="set-up-a-derived-credential-issuer"></a>Configurar un emisor de credenciales derivadas

Antes de crear directivas que requieran el uso de una credencial derivada, configure un emisor de credenciales en la consola de Intune. Un emisor de credenciales derivadas es una configuración aplicada a todo el inquilino. Los inquilinos solo admiten un emisor a la vez.

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Administración de inquilinos** > **Conectores y tokens** > **Credenciales derivadas**.

    > [!div class="mx-imgBorder"]
    > ![Configurar las credenciales derivadas en la consola](./media/derived-credentials/configure-provider.png)

3. Especifique un **nombre para mostrar** descriptivo para la directiva del emisor de credenciales derivadas.  Este nombre no se mostrará a los usuarios del dispositivo.

4. En **Emisor de credenciales derivadas**, seleccione el emisor de credenciales derivadas que ha elegido para su inquilino:
   - DISA Purebred (solo iOS)
   - Entrust Datacard
   - Intercede  

5. Especifique una **dirección URL de ayuda de credenciales derivadas** para proporcionar un vínculo a una ubicación que incluya instrucciones personalizadas para ayudar a los usuarios a obtener las credenciales derivadas para su organización. Las instrucciones deben ser específicas de su organización y del flujo de trabajo necesario para obtener una credencial del emisor elegido. El vínculo aparece en la aplicación Portal de empresa y debe ser accesible desde el dispositivo.

   Si no especifica su propia dirección URL, Intune proporcionará un vínculo a detalles genéricos que no pueden abarcar todos los escenarios. Puede que esta guía genérica no sea precisa para su entorno.

6. Seleccione una o más opciones para **Tipo de notificación**. Los tipos de notificación son los métodos que se usan para informar a los usuarios sobre los siguientes escenarios:

   - Inscribir un dispositivo con un emisor para obtener una credencial derivada nueva.
   - Obtener una credencial derivada nueva cuando la credencial actual está a punto de vencer.
   - Use una credencial derivada con un [objeto compatible](#supported-objects).

7. Cuando esté a punto, seleccione **Guardar** para completar la configuración del emisor de credenciales derivadas.

Después de guardar la configuración, puede hacer cambios en todos los campos excepto en *Emisor de credenciales derivadas*.  Para cambiar el emisor, vea [Cambiar el emisor de credenciales derivadas](#change-the-derived-credential-issuer).

## <a name="deploy-the-disa-purebred-app"></a>Implementar la aplicación DISA Purebred

*Esta sección solo se aplica si se usa DISA Purebred*.

Para usar **DISA Purebred** como emisor de credenciales derivadas para Intune, debe obtener la aplicación DISA Purebred y, después, usar Intune para implementar la aplicación en los dispositivos. Los usuarios del dispositivo usan la aplicación en su dispositivo para solicitar la credencial derivada de DISA Purebred.

Además de implementar la aplicación con Intune, configure una VPN por aplicación de Intune para la aplicación DISA Purebred.

**Lleve a cabo las siguientes tareas**:
  
1. Descargue la aplicación DISA Purebred: https:\//cyber.mil/pki-pke/purebred/.

2. Implemente la aplicación DISA Purebred en Intune. Vea [Incorporación de una aplicación de línea de negocio de iOS a Microsoft Intune](../apps/lob-apps-ios.md).

3. [Cree una VPN por aplicación](../configuration/vpn-settings-configure.md) para la aplicación DISA Purebred.

## <a name="use-derived-credentials-for-authentication-and-smime-signing-and-encryption"></a>Usar credenciales derivadas para la autenticación, la firma S/MIME y el cifrado

Puede especificar **credenciales derivadas** para los tipos de perfil y propósitos siguientes:

- [Aplicaciones](#use-derived-credentials-for-app-authentication)
- Correo electrónico:
  - [iOS e iPadOS](../configuration/email-settings-ios.md)
  - [Android Enterprise](../configuration/email-settings-android-enterprise.md)
- VPN:
  - [iOS e iPadOS](../configuration/vpn-settings-ios.md)
  - [Android Enterprise](../configuration/vpn-settings-android-enterprise.md)
- [Firma S/MIME y cifrado](certificates-s-mime-encryption-sign.md)
- Wi-Fi:
  - [iOS e iPadOS](../configuration/wi-fi-settings-ios.md)
  - [Android Enterprise](../configuration/wi-fi-settings-android-enterprise.md)

  En el caso de los perfiles de Wi-Fi, el *método de autenticación* solo está disponible si el **tipo de EAP** está establecido en uno de los siguientes valores:
  - EAP: TLS
  - EAP-TTLS
  - PEAP

### <a name="use-derived-credentials-for-app-authentication"></a>Usar credenciales derivadas para la autenticación de aplicaciones

Use credenciales derivadas para la autenticación basada en certificados en sitios web y aplicaciones. Para entregar una credencial derivada para la autenticación de aplicaciones:

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba los valores siguientes:

   Para iOS y iPadOS:
   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil es **Perfil Credencial derivada para dispositivos iOS**.
   - **Descripción**: escriba una descripción con información general sobre la configuración y otros detalles importantes.
   - **Plataforma**: Seleccione **iOS/iPad**.
   - **Tipo de perfil**: Seleccione **Credencial derivada**.

   Para Android Enterprise:
   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil es **Perfil Credencial derivada para dispositivos Android Enterprise**.
   - **Descripción**: escriba una descripción con información general sobre la configuración y otros detalles importantes.
   - **Plataforma**: seleccione **Android Enterprise**.
   - **Tipo de perfil**: en *Solo el propietario del dispositivo*, seleccione **Credencial derivada**.

4. Haga clic en **Aceptar** para guardar los cambios.
5. Cuando termine, seleccione **Aceptar** > **Crear** para crear el perfil de Intune. Una vez que se haya completado, el perfil se mostrará en la lista **Dispositivos - Perfiles de configuración**.
6. Seleccione su perfil nuevo > **Asignaciones**. Seleccione los grupos que deben recibir la directiva.

Los usuarios reciben la notificación por correo electrónico o de la aplicación en función de la configuración que haya especificado al configurar el emisor de credenciales derivadas. La notificación informa al usuario de que debe iniciar el Portal de empresa para que se puedan procesar las directivas de credenciales derivadas.

## <a name="renew-a-derived-credential"></a>Renovar una credencial derivada

Las credenciales derivadas no se pueden ampliar ni renovar; los usuarios deben usar el flujo de trabajo de solicitud de credenciales para solicitar una credencial derivada nueva para su dispositivo.

Si configura uno o varios métodos para el **tipo de notificación**, Intune notificará automáticamente a los usuarios cuando la credencial derivada actual haya alcanzado el 80% de su ciclo de vida. La notificación dirige a los usuarios al proceso de solicitud de credenciales para obtener una nueva credencial derivada.

Una vez que un dispositivo recibe una nueva credencial derivada, las directivas que usan credenciales derivadas se reimplementan en ese dispositivo.

## <a name="change-the-derived-credential-issuer"></a>Cambiar el emisor de credenciales derivadas

En el nivel de inquilino puede cambiar el emisor de credenciales, aunque solo se admite un emisor por inquilino a la vez.

Después de cambiar el emisor, se solicitará a los usuarios que obtengan una nueva credencial derivada del emisor nuevo. Deben hacerlo antes de poder usar una credencial derivada para la autenticación.

### <a name="change-the-issuer-for-your-tenant"></a>Cambiar el emisor de su inquilino

> [!IMPORTANT]
> Si elimina un emisor y acto seguido vuelve a configurar ese mismo emisor, deberá actualizar los perfiles y dispositivos para usar las credenciales derivadas de ese emisor. Las credenciales derivadas obtenidas antes de eliminar el emisor ya no son válidas.

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Administración de inquilinos** > **Conectores y tokens** > **Credenciales derivadas**.
3. Seleccione **Eliminar** para quitar el emisor de credenciales derivadas actual.
4. Configure un nuevo emisor.

### <a name="update-profiles-that-use-derived-credentials"></a>Actualizar los perfiles que usan credenciales derivadas

Después de eliminar un emisor y de agregar uno nuevo, edite todos los perfiles que usen credenciales derivadas. Esta regla se aplica incluso si se restaura el emisor anterior. Cualquier edición del perfil desencadenará una actualización, incluida una simple edición en la *descripción* del perfil.

### <a name="update-derived-credentials-on-devices"></a>Actualizar las credenciales derivadas en los dispositivos

Después de eliminar un emisor y de agregar uno nuevo, los usuarios del dispositivo deben solicitar una nueva credencial derivada. Esta regla se aplica incluso si se agrega el mismo emisor que se ha quitado. El proceso para solicitar la nueva credencial derivada es el mismo que para inscribir un dispositivo nuevo o renovar una credencial existente.

## <a name="next-steps"></a>Pasos siguientes

[Creación de perfiles de configuración de dispositivo](../configuration/device-profile-create.md).
