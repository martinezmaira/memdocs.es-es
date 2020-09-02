---
title: 'Configuración de características de dispositivos iOS/iPadOS en Microsoft Intune: Azure | Microsoft Docs'
description: Consulte todas las opciones para configurar AirPrint, el diseño de la pantalla principal, las notificaciones de aplicaciones, los dispositivos compartidos, el inicio de sesión único y la configuración de filtro de contenido web en Microsoft Intune en dispositivos iOS y iPadOS. Use estas opciones en un perfil de configuración de dispositivo para configurar en dispositivos iOS/iPadOS el uso de estas características de Apple en su organización.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ad78240aa9f2a1ef515be2635cfad0ce68e8ecc8
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909013"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>Configuración de dispositivos iOS/iPadOS para usar las características comunes de iOS/iPadOS en Intune

Intune incluye algunas configuraciones integradas para permitir que los usuarios de iOS/iPadOS usen diferentes características de Apple en sus dispositivos. Por ejemplo, puede controlar las impresoras AirPrint, agregar aplicaciones y carpetas a la base y páginas de la pantalla principal, mostrar notificaciones de aplicación, mostrar detalles de etiqueta de recursos en la pantalla de bloqueo, usar la autenticación de inicio de sesión único y usar la autenticación de certificados.

Use estas características para controlar los dispositivos iOS/iPadOS como parte de la solución de administración de dispositivos móviles (MDM).

En este artículo se enumeran estas opciones de configuración y se describe lo que hace cada una de ellas. Para más información sobre estas características, vaya a [Agregar la configuración de características de dispositivos iOS/iPadOS o macOS](device-features-configure.md).

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de características del dispositivo iOS/iPadOS](device-features-configure.md).

> [!NOTE]
> Esta configuración se aplica a diferentes tipos de inscripción, mientras que algunas opciones se aplican a todas las opciones de inscripción. Para más información sobre los diferentes tipos de inscripción, consulte [Inscripción en iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

> [!NOTE]
> Asegúrese de agregar todas las impresoras al mismo perfil. Apple evita que varios perfiles de AirPrint se dirijan al mismo dispositivo.

- **Dirección IP**: escriba la dirección IPv4 o IPv6 de la impresora. Si usa nombres de host para identificar impresoras, puede obtener la dirección IP haciendo ping a la impresora en el terminal. En la sección Obtención de la dirección IP y la ruta de acceso (en este artículo) se proporcionan más detalles.
- **Ruta de acceso**: La ruta de acceso suele ser `ipp/print` para las impresoras de la red. En la sección Obtención de la dirección IP y la ruta de acceso (en este artículo) se proporcionan más detalles.
- **Puerto**: escriba el puerto de escucha del destino de AirPrint. Si se deja esta propiedad en blanco, AirPrint usa el puerto predeterminado. Disponible en iOS 11.0+ y iPadOS 13.0+.
- **TLS**: **Habilitar** protege las conexiones AirPrint con Seguridad de la capa de transporte (TLS). Disponible en iOS 11.0+ y iPadOS 13.0+.

Para agregar servidores de AirPrint, puede:

- **Agregar** agrega el servidor AirPrint a la lista. Se pueden agregar muchos servidores de AirPrint.
- **Importe** un archivo separado por comas (.csv) con esta información. O bien, **Exportar** para crear una lista de los servidores de AirPrint que ha agregado.

### <a name="get-server-ip-address-resource-path-and-port"></a>Obtención de la dirección IP del servidor, la ruta de acceso de recursos y el puerto

Para agregar servidores AirPrinter, necesita la dirección IP de la impresora, la ruta de acceso de recursos y el puerto. Los pasos siguientes muestran cómo obtener esta información.

1. En un equipo Mac conectado a la misma red local (subred) que las impresoras AirPrint, abra **Terminal** (en **/Aplicaciones/Utilidades**).
2. En Terminal, escriba `ippfind` y seleccione Entrar.

    Anote la información de la impresora. Por ejemplo, puede devolver algo parecido a `ipp://myprinter.local.:631/ipp/port1`. La primera parte es el nombre de la impresora. La última parte (`ipp/port1`) es la ruta de acceso del recurso.

3. En Terminal, escriba `ping myprinter.local` y seleccione Entrar.

   Anote la dirección IP. Por ejemplo, puede devolver algo parecido a `PING myprinter.local (10.50.25.21)`.

4. Use los valores de dirección IP y de ruta de acceso del recurso. En este ejemplo, la dirección IP es `10.50.25.21` y la ruta de acceso del recurso es `/ipp/port1`.

## <a name="home-screen-layout"></a>Diseño de la pantalla principal

Esta característica se aplica a:

- iOS 9.3 o posterior
- IPadOS 13.0 y versiones más recientes

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

> [!NOTE]
> Agregue solo una aplicación al Dock, una página o una carpeta en una página. Si se agrega la misma aplicación en todos los lugares, se impide que la aplicación se vea en los dispositivos y se pueden mostrar errores de informes.
>
> Por ejemplo, si agrega la aplicación de cámara a un Dock y a una página, no se mostrará, y es posible que los informes muestren un error en la directiva. Para agregar la aplicación de cámara al diseño de la pantalla principal, elija solo el Dock o una página, no ambos.

### <a name="dock"></a>Acoplar

Use la configuración **Acoplar**, para agregar hasta seis elementos o carpetas a la base de la pantalla. Muchos dispositivos admiten menos elementos. Por ejemplo, los dispositivos iPhone admiten hasta cuatro elementos. En este caso, en los dispositivos solo se muestran los primeros cuatro elementos que agrega.

Puede agregar hasta **seis** elementos (aplicaciones y carpetas combinadas) para la base del dispositivo.

- **Agregar**: agrega aplicaciones o carpetas a la base de los dispositivos.
- **Tipo**: agregue una **Aplicación** o una **Carpeta**:

  - **Aplicación**: elija esta opción para agregar aplicaciones a la base en la pantalla. Especifique:

    - **Nombre de la aplicación**: escriba un nombre para la aplicación. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager. *No* se muestra en el dispositivo iOS/iPadOS.
    - **Identificador de lote de aplicaciones**: escriba el identificador de lote de la aplicación. Consulte [Identificadores de lote para aplicaciones iOS/iPadOS integradas](bundle-ids-built-in-ios-apps.md) para ver algunos ejemplos.

  - **Carpeta**: elija esta opción para agregar una carpeta a la base en la pantalla.

    Las aplicaciones que agrega a una página en una carpeta se organizan de izquierda a derecha y en el mismo orden que en la lista. Si agrega más aplicaciones de las que pueden caber en una página, se mueven a otra página.

    - **Nombre de la carpeta**: escriba el nombre de la carpeta. Este nombre se muestra en los dispositivos de los usuarios.
    - **Lista de páginas**: **agregue** una página y escriba las siguientes propiedades:

      - **Nombre de la página**: escriba un nombre para la página. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager. *No* se muestra en el dispositivo iOS/iPadOS.
      - **Nombre de la aplicación**: escriba un nombre para la aplicación. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager. *No* se muestra en el dispositivo iOS/iPadOS.
      - **Identificador de lote de aplicaciones**: escriba el identificador de lote de la aplicación. Consulte [Identificadores de lote para aplicaciones iOS/iPadOS integradas](bundle-ids-built-in-ios-apps.md) para ver algunos ejemplos.

      Puede agregar hasta **20** páginas para base del dispositivo.

> [!NOTE]
> Al usar la configuración de diseño de pantalla principal para agregar las páginas, o bien agregar las páginas y aplicaciones a la base, se bloquean los iconos de la pantalla principal y las páginas. No se pueden mover ni eliminar. Este comportamiento puede deberse al diseño con iOS/iPadOS y las directivas MDM de Apple.

#### <a name="example"></a>Ejemplo

En el ejemplo siguiente, en la pantalla del Dock se muestran las aplicaciones Safari, Correo y Bolsa. Se ha seleccionado la aplicación Correo para mostrar sus propiedades:

> [!div class="mx-imgBorder"]
> ![Ejemplo de configuración del Dock en el diseño de la pantalla principal de iOS/iPadOS en Intune](./media/ios-device-features-settings/dock-screen-mail-app.png)

Cuando asigna la directiva a un iPhone, la base tiene un aspecto similar al de la siguiente imagen:

> [!div class="mx-imgBorder"]
> ![Diseño de ejemplo de la base de iOS/iPadOS en iPhone](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>Páginas

Agregue las páginas que quiere que aparezcan en la pantalla principal y las aplicaciones que desea que se muestren en cada página. Las aplicaciones que agrega a una página se organizan de izquierda a derecha, en el mismo orden que en la lista. Si agrega más aplicaciones de las que pueden caber en una página, se mueven a otra página.

> [!TIP]
> Para reordenar elementos en cualquier pantalla principal y listas de páginas, puede arrastrarlos y soltarlos.

Puede agregar hasta **40** páginas en un dispositivo.

- **Lista de páginas**: **agregue** una página y escriba las siguientes propiedades:

  - **Nombre de la página**: escriba un nombre para la página. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager y *no* se muestra en el dispositivo iOS/iPadOS.

  Puede agregar hasta **60** elementos (aplicaciones y carpetas combinadas) en un dispositivo.

  - **Agregar**: agrega aplicaciones o carpetas a una página de los dispositivos.

    - **Tipo**: agregue una **Aplicación** o una **Carpeta**:

      - **Aplicación**: elija esta opción para agregar aplicaciones a una página en la pantalla. Indique también:

        - **Nombre de la aplicación**: escriba un nombre para la aplicación. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager. *No* se muestra en el dispositivo iOS/iPadOS.
        - **Identificador de lote de aplicaciones**: escriba el identificador de lote de la aplicación. Consulte [Identificadores de lote para aplicaciones iOS/iPadOS integradas](bundle-ids-built-in-ios-apps.md) para ver algunos ejemplos.

      - **Carpeta**: elija esta opción para agregar una carpeta a la base en la pantalla.

        Las aplicaciones que agrega a una página en una carpeta se organizan de izquierda a derecha y en el mismo orden que en la lista. Si agrega más aplicaciones de las que pueden caber en una página, se mueven a otra página.

        - **Nombre de la carpeta**: escriba un nombre para la carpeta. Este nombre se muestra en los dispositivos de los usuarios.
        - **Agregar**: agrega páginas a la carpeta. Además, escriba las propiedades siguientes:

          - **Nombre de la página**: escriba un nombre para la página. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager. *No* se muestra en el dispositivo iOS/iPadOS.
          - **Nombre de la aplicación**: escriba un nombre para la aplicación. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager. *No* se muestra en el dispositivo iOS/iPadOS.
          - **Identificador de lote de aplicaciones**: escriba el identificador de lote de la aplicación. Consulte [Identificadores de lote para aplicaciones iOS/iPadOS integradas](bundle-ids-built-in-ios-apps.md) para ver algunos ejemplos.

#### <a name="example"></a>Ejemplo

En el ejemplo siguiente, se agrega una nueva página denominada **Contoso**. En la página se muestran las aplicaciones Buscar a mis amigos y Ajustes:

> [!div class="mx-imgBorder"]
> ![Diseño de la pantalla principal de iOS/iPadOS, nueva página Ajustes y ejemplo en Intune](./media/ios-device-features-settings/page-find-friends-settings-apps.png)

Se ha seleccionado la aplicación Ajustes para mostrar sus propiedades:

> [!div class="mx-imgBorder"]
> ![Ejemplo de propiedades de la aplicación Ajustes en el diseño de la pantalla principal de iOS/iPadOS en Intune](./media/ios-device-features-settings/page-settings-app-properties.png)

Cuando asigna la directiva a un iPhone, la página tiene un aspecto similar al de la siguiente imagen:

> [!div class="mx-imgBorder"]
> ![Dispositivo iOS/iPadOS con la pantalla principal modificada en Intune](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>Notificaciones de la aplicación

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Agregar**: agregue notificaciones para las aplicaciones:

  > [!div class="mx-imgBorder"]
  > ![Adición de notificaciones de aplicación en el perfil de iOS/iPadOS en Intune](./media/ios-device-features-settings/ios-ipados-app-notifications.png)

  - **Identificador de lote de aplicaciones**: escriba un identificador en **Identificador del lote de aplicaciones** para la aplicación que desea agregar. Consulte [Identificadores de lote para aplicaciones iOS/iPadOS integradas](bundle-ids-built-in-ios-apps.md) para ver algunos ejemplos.
  - **Nombre de la aplicación**: escriba el nombre de la aplicación que desea agregar. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager. *No* se muestra en los dispositivos.
  - **Publicador**: escriba el publicador de la aplicación que está agregando. Este nombre se usa como referencia en el centro de administración de Microsoft Endpoint Manager. *No* se muestra en los dispositivos.
  - **Notificaciones**: puede seleccionar **Habilitar** o **Deshabilitar** para que la aplicación envíe o no, respectivamente, notificaciones a los dispositivos.
    - **Mostrar en Centro de notificaciones**: **Habilitar** permite a la aplicación mostrar notificaciones en el centro de notificaciones del dispositivo. **Deshabilitar** impide a la aplicación mostrar notificaciones en el centro de notificaciones.
    - **Mostrar en pantalla de bloqueo**: **Habilitar** muestra las notificaciones de la aplicación en la pantalla de bloqueo del dispositivo. **Deshabilitar** impide a la aplicación mostrar notificaciones en la pantalla de bloqueo.
    - **Tipo de alerta**: cuando los dispositivos están desbloqueados, elija cómo se muestra la notificación. Las opciones son:
      - **Ninguna**: no se muestra ninguna notificación.
      - **Banner**: se muestra brevemente un banner con la notificación.
      - **Modal**: se muestra la notificación y los usuarios deben descartarla manualmente para poder seguir usando el dispositivo.
    - **Distintivo en el icono de la aplicación**: seleccione **Habilitar** para agregar un distintivo en el icono de la aplicación. El distintivo significa que la aplicación envió una notificación.
    - **Sonidos**: seleccione **Habilitar** para reproducir un sonido cuando se entrega una notificación.

## <a name="lock-screen-message"></a>Mensaje de la pantalla de bloqueo

Esta característica se aplica a:

- iOS 9.3 y versiones posteriores
- IPadOS 13.0 y versiones más recientes

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Información de etiqueta de activo**: escriba información sobre la etiqueta de activo del dispositivo. Por ejemplo, escriba `Owned by Contoso Corp` o `Serial Number: {{serialnumber}}`.

  El texto que escriba se mostrará en la ventana de inicio de sesión y en la pantalla de bloqueo de los dispositivos.

- **Nota al pie de pantalla de bloqueo**: si pierde el dispositivo o se lo roban, escriba una nota que pueda ayudar a que se lo devuelvan. Puede escribir el texto que quiera. Por ejemplo, escriba algo parecido a `If found, call Contoso at ...`.

  Los tokens de dispositivo también se pueden usar para agregar información específica sobre el dispositivo a estos campos. Por ejemplo, para que se muestre el número de serie, escriba `Serial Number: {{serialnumber}}` o `Device ID: {{DEVICEID}}`. En la pantalla de bloqueo, el texto tendrá un aspecto similar a este: `Serial Number 123456789ABC`. Al especificar variables, no olvide usar llaves: `{{ }}`. En los [tokens de configuración de aplicación](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) podrá ver una lista de las variables que puede usar. También puede usar `DEVICENAME` o cualquier otro valor específico del dispositivo.

  > [!NOTE]
  > Las variables no se validan en la interfaz de usuario y distinguen mayúsculas de minúsculas. Como resultado, es posible que vea perfiles guardados con entradas incorrectas. Por ejemplo, si escribe `{{DeviceID}}` en lugar de `{{deviceid}}` o "{{DEVICEID}}", se muestra la cadena literal en lugar del identificador único del dispositivo. Asegúrese de especificar la información correcta. Se admiten todas las variables en minúsculas o mayúsculas, pero no una mezcla de ambas. 

## <a name="single-sign-on"></a>Inicio de sesión único

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Dominio kerberos**: escriba la parte del dominio de la dirección URL. Por ejemplo, escriba `contoso.com`.
- **Nombre principal de Kerberos**: Intune busca este atributo para cada usuario de Azure AD. Después, Intune rellena el campo correspondiente (como UPN) antes de generar el código XML que se instala en los dispositivos. Las opciones son:

  - **No configurado**: Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo solicitará a los usuarios un nombre de entidad de seguridad de Kerberos cuando se implemente el perfil en los dispositivos. Se requiere un nombre de entidad de seguridad para que las MDM instalen perfiles de SSO.
  - **Nombre principal de usuario**: se analiza el UPN de la manera siguiente:

    > [!div class="mx-imgBorder"]
    > ![Atributo SSO de nombre de usuario de iOS/iPadOS en Intune](./media/ios-device-features-settings/User-name-attribute.png)

    También puede sobrescribir el dominio kerberos con el texto que escriba en el cuadro de texto **Dominio kerberos**.

    Por ejemplo, Contoso tiene varias regiones, incluidas Europa, Asia y Norteamérica. Contoso desea que los usuarios de Asia usen el inicio de sesión único y la aplicación requiere UPN con el formato `username@asia.contoso.com`. Si selecciona **Nombre principal de usuario**, el dominio kerberos de cada usuario se toma de Azure AD, que es `contoso.com`. Por tato, para los usuarios de Asia, seleccione **Nombre principal de usuario** y escriba `asia.contoso.com`. El UPN del usuario se convierte en `username@asia.contoso.com`, en lugar de `username@contoso.com`.

  - **Identificador de dispositivo de Intune** : Intune selecciona automáticamente el identificador de dispositivo de Intune.

    De forma predeterminada, las aplicaciones solo tienen que usar el identificador de dispositivo. Pero si la aplicación usa el dominio kerberos y el identificador de dispositivo, puede escribir dicho dominio en el cuadro de texto **Dominio Kerberos**.

    > [!NOTE]
    > Si usa el identificador de dispositivo, mantenga vacío el dominio kerberos de forma predeterminada.

  - **Id. de dispositivo de Azure AD**
  - **Nombre de cuenta SAM**: Intune rellena el nombre de la cuenta del Administrador de cuentas de seguridad (SAM) local.


- **Aplicaciones**: **agregue** las aplicaciones de los dispositivos de los usuarios que pueden usar el inicio de sesión único.

  La matriz `AppIdentifierMatches` debe incluir cadenas que coincidan con los identificadores del lote de aplicaciones. Estas cadenas pueden ser coincidencias exactas, como `com.contoso.myapp`, o pueden especificar una coincidencia de prefijo en el identificador de lote mediante el carácter comodín \*. El carácter comodín debe aparecer después de un carácter de punto (.) y solo puede hacerlo una vez, al final de la cadena, como `com.contoso.*`. Cuando se incluye un carácter comodín, se concede acceso a la cuenta a cualquier aplicación cuyo identificador de lote empiece por el prefijo.

  Use **Nombre de la aplicación** para especificar un nombre descriptivo que ayude a identificar el identificador de lote.

- **Prefijos de dirección URL**: **Agregue** cualquier dirección URL de la organización que exija la autenticación de inicio de sesión único de usuario.

  Por ejemplo, cuando un usuario se conecta a alguno de estos sitios, el dispositivo iOS/iPadOS usa las credenciales de inicio de sesión único. Los usuarios no tienen que escribir otras credenciales. Si la autenticación multifactor está habilitada, los usuarios tienen que escribir la segunda autenticación.

  > [!NOTE]
  > Estas direcciones URL deben tener el formato FQDN correcto. Apple exige que tengan el formato `http://<yourURL.domain>`.

  Los patrones de coincidencia de la dirección URL deben comenzar por `http://` o `https://`. Se ejecuta una coincidencia de cadena simple, así que el prefijo de dirección URL `http://www.contoso.com/` no coincide con `http://www.contoso.com:80/`. Con iOS 10.0+ y iPadOS 13.0+, se puede usar un único carácter comodín \* para especificar todos los valores coincidentes. Por ejemplo, `http://*.contoso.com/` coincide con `http://store.contoso.com/` y con `http://www.contoso.com`.

  Los patrones `http://.com` y `https://.com` coinciden con todas las direcciones URL HTTP y HTTPS, respectivamente.

- **Certificado de renovación**: si usa certificados para la autenticación (no contraseñas), seleccione el certificado SCEP o PFX existente como certificado de autenticación. Normalmente, se trata del mismo certificado implementado en los usuarios para otros perfiles como VPN, Wi-Fi o correo electrónico.

## <a name="web-content-filter"></a>Filtro de contenido web

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Tipo de filtro**: seleccione esta opción para permitir sitios web específicos. Las opciones son:

  - **Configurar URL**: use el filtro web integrado de Apple que busca términos para adultos, incluido el lenguaje obsceno y sexualmente explícito. Esta característica evalúa cada página web cuando se carga e identifica y bloquea contenido inadecuado. También puede agregar direcciones URL que no desea que el filtro compruebe. O bien, puede bloquear direcciones URL específicas, independientemente de la configuración del filtro de Apple.

    - **URL permitidas**: **agregue** las direcciones URL que desea permitir. Estas direcciones URL no son capturadas por el filtro web de Apple.

        > [!NOTE]
        > Las direcciones URL que especifique son las direcciones URL que no desea que el filtro web de Apple evalúe. Estas direcciones URL no son una lista de sitios web permitidos. Para crear una lista de sitios web permitidos, establezca **Tipo de filtro** en **Solo sitios web específicos**.

    - **URL bloqueadas**: **agregue** las direcciones URL que desea impedir que se abran, independientemente de la configuración de filtro web de Apple.

  - **Solo sitios web específicos** (solo para el explorador web Safari): estas direcciones URL se agregan a los marcadores del explorador Safari. Los usuarios **solo** tienen permiso para visitar estos sitios; no se pueden abrir otros sitios. Use esta opción solo si conoce la lista exacta de direcciones URL a las que pueden acceder los usuarios.

    - **Dirección URL**: escriba la dirección URL del sitio web que quiere permitir. Por ejemplo, escriba `https://www.contoso.com`.
    - **Ruta de acceso de marcador**: Apple ha cambiado esta configuración. Todos los marcadores van a la carpeta **Sitios aprobados**. Los marcadores no entran en la ruta de acceso de marcador que especifique.
    - **Título**: escriba un título descriptivo para el marcador.

    Si no especifica ninguna dirección URL, los usuarios no pueden acceder a ningún sitio web, excepto `microsoft.com`, `microsoft.net` y `apple.com`. Intune permite automáticamente estas direcciones URL.

## <a name="single-sign-on-app-extension"></a>Extensión de aplicación de inicio de sesión único

Esta característica se aplica a:

- iOS 13.0 y versiones posteriores
- iPadOS 13.0 y versiones posteriores

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Tipo de extensión de la aplicación de SSO**: elija el tipo de extensión de la aplicación de SSO. Las opciones son:

  - **No configurado**: Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo no usará extensiones de la aplicación. Para deshabilitar una extensión de la aplicación, puede cambiar el tipo de extensión de la aplicación de SSO a **No configurado**.
  - **Microsoft Azure AD**: usa el complemento de Microsoft Enterprise Single Sign-On, que es una extensión de la aplicación de SSO de tipo redirección. Este complemento proporciona SSO para las cuentas de Active Directory en todas las aplicaciones compatibles con la característica [Enterprise Single Sign-On de Apple](https://developer.apple.com/documentation/authenticationservices). Use este tipo de extensión de la aplicación de SSO para habilitar el inicio de sesión único en las aplicaciones de Microsoft, las aplicaciones de la organización y los sitios web que se autentican mediante Azure AD.

    El complemento de SSO actúa como agente de autenticación avanzado que ofrece mejoras en la seguridad y la experiencia del usuario. Todas las aplicaciones que usaron Microsoft Authenticator seguirán obteniendo el inicio de sesión único con el [complemento Microsoft Enterprise Single Sign-On de los dispositivos Apple](/azure/active-directory/develop/apple-sso-plugin).

    > [!IMPORTANT]
    > Para lograr el inicio de sesión único con el tipo de extensión de la aplicación de SSO de Microsoft Azure AD, instale en primer lugar la aplicación Microsoft Authenticator de iOS/iPadOS en los dispositivos. La aplicación Authenticator entrega el complemento de Microsoft Enterprise Single Sign-On a los dispositivos y la configuración de la extensión de la aplicación de SSO de MDM activa el complemento. Una vez que Authenticator y el perfil de extensión de la aplicación de SSO están instalados en los dispositivos, los usuarios deben escribir sus credenciales para iniciar sesión y establecer una sesión en los dispositivos. Esta sesión se usa a continuación en aplicaciones diferentes sin necesidad de que los usuarios se autentiquen de nuevo. Para obtener más información sobre Authenticator, vea [Qué es la aplicación Microsoft Authenticator](/azure/active-directory/user-help/user-help-auth-app-overview).

  - **Redireccionamiento**: use una extensión de la aplicación de redireccionamiento genérica y personalizable para usar SSO con flujos de autenticación modernos. Asegúrese de que conoce el identificador de la extensión de la aplicación de su organización.
  - **Credenciales**: use una extensión de la aplicación de credenciales genérica y personalizable para realizar el inicio de sesión único con flujos de autenticación de desafío y respuesta. Asegúrese de que conoce el identificador de la extensión de la aplicación de su organización.
  - **Kerberos**: use la extensión integrada de Kerberos de Apple, que se incluye en iOS 13.0 y iPadOS 13.0, y versiones posteriores. Esta opción es una versión específica de Kerberos de la extensión de la aplicación de **Credenciales**.

  > [!TIP]
  > Con los tipos **Redireccionamiento** y **Credenciales**, se agregan sus propios valores de configuración para pasar a través de la extensión. Si utiliza **Credenciales**, considere la posibilidad de usar las opciones de configuración integradas proporcionadas por Apple en el tipo **Kerberos**.

- **Modo de dispositivo compartido** (solo Microsoft Azure AD): elija **Habilitar** si se va a implementar el complemento de Microsoft Enterprise Single Sign-On en dispositivos iOS/iPados configurados para la característica de modo de dispositivo compartido de Azure AD. Los dispositivos en modo compartido permiten a muchos usuarios iniciar sesión de forma global y fuera de las aplicaciones que admiten el modo de dispositivo compartido. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración. De forma predeterminada, los dispositivos iOS/iPad no están diseñados para compartirse entre varios usuarios.

  Para obtener más información sobre el modo de dispositivo compartido y cómo habilitarlo, vea [Información general del modo de dispositivo compartido](/azure/active-directory/develop/msal-shared-devices) y [Modo de dispositivo compartido para dispositivos iOS](/azure/active-directory/develop/msal-ios-shared-devices).  

  Esta característica se aplica a:
  
  - iOS/iPadOS 13.5 y versiones más recientes

- **Id. de extensión** (redireccionamiento y credenciales): escriba el identificador de lote que identifica la extensión de la aplicación de SSO, como `com.apple.extensiblesso`.

- **Id. de equipo** (redireccionamiento y credenciales): escriba el identificador de equipo de la extensión de la aplicación de SSO. Un identificador de equipo es una cadena alfanumérica de 10 caracteres (números y letras) que Apple genera, como `ABCDE12345`. El identificador del equipo no es obligatorio.

  En [Búsqueda del identificador de equipo](https://help.apple.com/developer-account/#/dev55c3c710c) (se abre el sitio web de Apple) puede encontrar más información.

- **Dominio** (credenciales y Kerberos): escriba el nombre del dominio de autenticación. El nombre de dominio debe escribirse en mayúsculas, por ejemplo, `CONTOSO.COM`. Normalmente, el nombre de dominio es el mismo que el nombre de dominio DNS, pero en mayúsculas.

- **Dominios** (credenciales y Kerberos): escriba los nombres de dominio o host de los sitios que pueden autenticarse mediante SSO. Por ejemplo, si el sitio web es `mysite.contoso.com`, `mysite` es el nombre de host y `contoso.com` es el nombre de dominio. Cuando los usuarios se conectan a cualquiera de estos sitios, la extensión de la aplicación controla el desafío de autenticación. Esta autenticación permite a los usuarios usar Face ID, Touch ID o el código PIN/código de acceso de Apple para iniciar sesión.

  - Todos los dominios de los perfiles de Intune de la extensión de la aplicación de inicio de sesión único deben ser exclusivos. No se puede repetir un dominio en ningún perfil de extensión de la aplicación de inicio de sesión, aunque se usen distintos tipos de extensiones de la aplicación de SSO.
  - Estos dominios no distinguen mayúsculas de minúsculas.

- **Direcciones URL** (solo redireccionamiento): escriba los prefijos de dirección URL de los proveedores de identidades en cuyo nombre la extensión de la aplicación de redireccionamiento usa el inicio de sesión único. Cuando los usuarios se redirige a estas direcciones URL, la extensión de la aplicación de inicio de sesión único interviene y solicita el inicio de sesión único.

  - Todas las direcciones URL de los perfiles de extensión de la aplicación de inicio de sesión único de Intune deben ser únicas. No se puede repetir un dominio en ningún perfil de extensión de la aplicación de SSO, aunque se usen distintos tipos de extensiones de la aplicación de SSO.
  - Las direcciones URL deben comenzar por `http://` or `https://`.

- **Configuración adicional** (Microsoft Azure AD, redireccionamiento y credenciales): escriba datos adicionales específicos de la extensión para pasarlos a la extensión de la aplicación de SSO:
  - **Clave**: escriba el nombre del elemento que quiere agregar, como `user name`.
  - **Tipo**: escriba el tipo de datos. Las opciones son:

    - String
    - Booleano: en **Valor de configuración**, escriba `True` o `False`.
    - Entero: en **Valor de configuración**, escriba un número.

  - **Valor**: escriba los datos.

  - **Agregar**: seleccione esta opción para agregar las claves de configuración.

- **Uso de la cadena de claves** (solo Kerberos): **Bloquear** impide que las contraseñas se guarden y almacenen en la cadena de claves. Si está bloqueado, no se le pedirá a los usuarios que guarde la contraseña y tendrá que volver a escribirla cuando expire el vale de Kerberos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir guardar y almacenar las contraseñas en la cadena de claves. No se pedirá a los usuarios que vuelvan a escribir la contraseña cuando expire el vale.
- **Face ID, Touch ID o código de acceso** (solo Kerberos): **Requerir** obliga a los usuarios a usar su Face ID, Touch ID o código de acceso del dispositivo cuando se necesitan las credenciales para actualizar el vale de Kerberos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no exigir que los usuarios usen información biométrica o el código de acceso del dispositivo para actualizar el vale de Kerberos. Si **Uso de la cadena de claves** está bloqueado, no se aplica esta configuración.
- **Dominio predeterminado** (solo Kerberos): **Habilitar** establece el valor de **Dominio** que escribió como dominio predeterminado. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no establecer un dominio Kerberos predeterminado.

  > [!TIP]
  > - **Habilite** esta opción si va a configurar varias extensiones de la aplicación de SSO de Kerberos en su organización.
  > - **Habilite** esta opción si usa varios dominios. Establece el valor de **Dominio** que escribió como dominio predeterminado.
  > - Si solo tiene un dominio, déjelo como **No configurado** (valor predeterminado).

- **Nombre de la entidad de seguridad** (solo Kerberos): escriba el nombre de usuario de la entidad de seguridad de Kerberos. No es necesario incluir el nombre de dominio. Por ejemplo, en `user@contoso.com`, `user` es el nombre de la entidad de seguridad y `contoso.com` es el nombre de dominio.

  > [!TIP]
  > - También puede usar variables en el nombre de la entidad de seguridad mediante llaves `{{ }}`. Por ejemplo, para mostrar el nombre de usuario, escriba `Username: {{username}}`. 
  > - Sin embargo, tenga cuidado con la sustitución de variables porque estas no se validan en la interfaz de usuario y distinguen mayúsculas de minúsculas. Asegúrese de especificar la información correcta.

- **Código de sitio de Active Directory** (solo Kerberos): escriba el nombre del sitio de Active Directory que la extensión de Kerberos debe usar. Es posible que no necesite cambiar este valor, ya que la extensión de Kerberos puede encontrar automáticamente el código del sitio de Active Directory.
- **Nombre de la caché** (solo Kerberos): escriba el nombre de los servicios de seguridad genéricos (GSS) de la memoria caché de Kerberos. Lo más probable es que no tenga que establecer este valor.
- **Identificadores de lote de aplicaciones** (Microsoft Azure AD, Kerberos): escriba los identificadores de lote de las aplicaciones adicionales que deben obtener el inicio de sesión único mediante una extensión en los dispositivos.

  Si va a usar el tipo de extensión de aplicación de inicio de sesión único de Microsoft Azure AD, estas aplicaciones emplean el complemento Microsoft Enterprise Single Sign-On para autenticar al usuario sin necesidad de un inicio de sesión. Los identificadores de lote de aplicaciones que especifique tienen permiso para usar la extensión de aplicación de inicio de sesión único de Microsoft Azure AD si no utilizan bibliotecas de Microsoft, como la de autenticación de Microsoft (MSAL). La experiencia en estas aplicaciones podría no ser tan fluida como con las bibliotecas de Microsoft. Las aplicaciones antiguas que usan la autenticación de MSAL, o las aplicaciones que no usan las bibliotecas de Microsoft más recientes, deben agregarse a esta lista para que funcionen correctamente con la extensión de aplicación de inicio de sesión único de Microsoft Azure.  

  Si va a usar el tipo de extensión de aplicación de inicio de sesión único de Kerberos, estas aplicaciones tienen acceso al vale de concesión de vales de Kerberos y al vale de autenticación, y autentican a los usuarios en los servicios a los que tienen acceso autorizado.

- **Asignación de dominio** (solo Kerberos): **agregue** los sufijos DNS de dominio que se deben asignar al dominio. Use esta opción cuando los nombres DNS de los hosts no coincidan con el nombre de dominio. Lo más probable es que no tenga que crear esta asignación personalizada de dominio a dominio.
- **Certificado PKINIT** (solo Kerberos): **seleccione** el certificado de criptografía de clave pública de la autenticación inicial (PKINIT) que se puede usar en la autenticación Kerberos. Puede elegir entre los certificados [PKCS](../protect/certficates-pfx-configure.md) o [SCEP](../protect/certificates-scep-configure.md) que ha agregado en Intune. Para más información sobre los certificados, consulte [Uso de certificados para la autenticación en Microsoft Intune](../protect/certificates-configure.md).

## <a name="wallpaper"></a>Fondo de pantalla

Puede experimentar un comportamiento inesperado cuando un perfil sin imagen se asigna a dispositivos con una imagen existente. Por ejemplo, crea un perfil sin una imagen. Este perfil se asigna a dispositivos que ya tienen una imagen. En este escenario, la imagen puede cambiar a la predeterminada del dispositivo, o bien la imagen original puede permanecer en el dispositivo. Este comportamiento se controla y limita por medio de la plataforma MDM de Apple.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Ubicación de presentación del fondo de pantalla**: elija una ubicación en los dispositivos para mostrar la imagen. Las opciones son:
  - **No configurado**: Intune no cambia ni actualiza esta configuración. no se agrega una imagen personalizada a los dispositivos. De forma predeterminada, el sistema operativo podría establecer su propia imagen.
  - **Pantalla de bloqueo**: agrega la imagen a la pantalla de bloqueo.
  - **Pantalla de inicio**: agrega la imagen a la pantalla de inicio.
  - **Pantalla de bloqueo y pantalla de inicio**: usa la misma imagen en la pantalla de bloqueo y en la pantalla de inicio.
- **Imagen de fondo de pantalla**: cargue una imagen .png, .jpg o .jpeg existente que desee usar. Asegúrese de que el tamaño del archivo es inferior a 750 KB. También puede **quitar** una imagen que ha agregado.

> [!TIP]
> Para mostrar diferentes imágenes en la pantalla de bloqueo y en la pantalla de inicio, cree un perfil con la imagen de la pantalla de bloqueo. Cree otro perfil con la imagen de la pantalla de inicio. Asigne ambos perfiles a los grupos de usuarios o dispositivos iOS/iPadOS.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede crear perfiles de característica de dispositivo para dispositivos [macOS](macos-device-features-settings.md).