---
title: Administración de Edge para iOS y Android con Intune
titleSuffix: ''
description: Use las directivas de configuración y protección de aplicaciones de Intune con Edge para iOS y Android a fin de garantizar que siempre se apliquen medidas de seguridad al acceder a los sitios web corporativos.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/08/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa70da636d619a52c0ec8591a43e85e11ff7f9f2
ms.sourcegitcommit: 86c2c438fd2d87f775f23a7302794565f6800cdb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2020
ms.locfileid: "86410902"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>Administración del acceso web mediante Edge para iOS y Android con Microsoft Intune

Edge para iOS y Android está diseñado para permitir a los usuarios explorar la web y es compatible con varias identidades. Los usuarios pueden agregar una cuenta profesional, así como una cuenta personal, para realizar la exploración. Existe una separación completa entre las dos identidades, igual que en otras aplicaciones móviles de Microsoft.

Edge para iOS es compatible con iOS 12.0 y versiones posteriores. Edge para Android es compatible con Android 5 y versiones posteriores.

> [!NOTE]
> Edge para iOS y Android no usa la configuración establecida por los usuarios para el explorador nativo en sus dispositivos, porque Edge para iOS y Android no puede acceder a esta configuración.

Tendrá a su disposición las capacidades de protección más enriquecidas y más amplias para los datos de Office 365 cuando se suscriba al conjunto de aplicaciones de Enterprise Mobility + Security, que incluye características de Microsoft Intune y Azure Active Directory Premium, como el acceso condicional. Como mínimo, le interesará implementar una directiva de acceso condicional que solo permita la conectividad a Edge para iOS y Android desde dispositivos móviles y una directiva de protección de aplicaciones de Intune que garantice que la experiencia de exploración esté protegida.

> [!NOTE]
> Los nuevos clips web (aplicaciones web ancladas) de los dispositivos iOS se abrirán en Edge para iOS y Android, en lugar de en Intune Managed Browser, si tienen que abrirse en un explorador protegido. En el caso de los clips web de iOS más antiguos, debe cambiar el destino de estos clips web para asegurarse de que se abren en Edge para iOS y Android, y no en Managed Browser.

## <a name="apply-conditional-access"></a>Aplicación del acceso condicional
Las organizaciones pueden usar directivas de acceso condicional de Azure AD para asegurarse de que los usuarios solo puedan acceder al contenido profesional o educativo mediante Edge para iOS y Android. Para ello, necesitará una directiva de acceso condicional destinada a todos los usuarios potenciales. Encontrará más información sobre la creación de esta directiva en [Uso obligatorio de directivas de protección de aplicaciones para el acceso a aplicaciones en la nube con acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Siga el [Escenario 2: Las aplicaciones de explorador requieren aplicaciones aprobadas con directivas de protección de aplicaciones](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies), lo que permite Edge para iOS y Android, pero impide que otros exploradores web de dispositivos móviles se conecten a los puntos de conexión de Office 365.

   >[!NOTE]
   > Esta directiva garantiza que los usuarios móviles puedan acceder a todos los puntos de conexión de Office 365 desde Edge para iOS y Android. Esta Directiva también impide que los usuarios empleen InPrivate para acceder a los puntos de conexión de Office 365.

Con el acceso condicional, también puede establecer como destino sitios locales que haya expuesto a usuarios externos a través del [proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="create-intune-app-protection-policies"></a>Creación de directivas de protección de aplicaciones de Intune

Las directivas de protección de aplicaciones (APP) definen qué aplicaciones están permitidas y qué acciones pueden llevar a cabo con los datos de la organización. Las opciones disponibles en APP permiten a las organizaciones adaptar la protección a sus necesidades específicas. Para algunas de ellas, puede que no sea obvio qué configuración de directivas es necesaria para implementar un escenario completo. Para ayudar a las organizaciones a priorizar la protección del punto de conexión del cliente móvil, Microsoft ha introducido la taxonomía para su marco de protección de datos de APP para la administración de aplicaciones móviles de iOS y Android.

El marco de protección de datos de APP se organiza en tres niveles de configuración distintos, cada uno de ellos basado en el nivel anterior:

- La **protección de datos empresariales básica** (nivel 1) garantiza que las aplicaciones estén protegidas con un PIN y cifradas, y realiza operaciones de borrado selectivo. En el caso de los dispositivos Android, este nivel valida la certificación de dispositivos Android. Se trata de una configuración de nivel de entrada que proporciona un control de protección de datos similar en las directivas de buzón de Exchange Online y que introduce tecnologías informáticas y el rellenado de usuarios en APP.
- La **protección de datos empresariales mejorada** (nivel 2) incorpora mecanismos para la prevención de la pérdida de datos de APP y requisitos mínimos para el sistema operativo. Esta es la configuración aplicable a la mayoría de los usuarios móviles que acceden a datos profesionales o educativos.
- La **protección de datos empresariales alta** (nivel 3) incorpora mecanismos avanzados para la protección de datos, configuración de PIN mejorada y defensa contra amenazas móviles de APP. Esta configuración es conveniente para los usuarios que acceden a datos de alto riesgo.

Para ver las recomendaciones específicas para cada nivel de configuración y las aplicaciones mínimas que se deben proteger, revise el [Marco de protección de datos mediante directivas de protección de aplicaciones](app-protection-framework.md).

Independientemente de si el dispositivo está inscrito en una solución de administración de puntos de conexión unificada (UEM), es necesario crear una directiva de protección de aplicaciones de Intune para las aplicaciones iOS y Android con los pasos descritos en [Creación y asignación de directivas de protección de aplicaciones](app-protection-policies.md). Estas directivas deben cumplir como mínimo las siguientes condiciones:

1. Deben incluir todas las aplicaciones para dispositivos móviles de Microsoft 365, como Outlook, OneDrive, Office o Teams, ya que esto garantizará que los usuarios puedan acceder a los datos profesionales o educativos, y manipularlos desde cualquier aplicación de Microsoft de forma segura.

2. Deben asignarse a todos los usuarios. Esto garantiza que todos los usuarios estén protegidos, independientemente de si usan Edge para iOS o Android.

3. Deben determinar qué nivel de marco cumple los requisitos. La mayoría de las organizaciones deben implementar la configuración definida en la **protección de datos empresariales mejorada** (nivel 2), ya que habilita los controles de protección de datos y de requisitos de acceso.

Para obtener más información sobre las configuraciones disponibles, vea [Configuración de directivas de protección de aplicaciones Android](app-protection-policy-settings-android.md) y [Configuración de directivas de protección de aplicaciones iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Para aplicar directivas de protección de aplicaciones de Intune a aplicaciones en dispositivos Android que no están inscritos en Intune, el usuario también debe instalar el Portal de empresa de Intune. Para obtener más información, vea [Qué esperar cuando la aplicación Android está administrada por directivas de protección de aplicaciones](../fundamentals/end-user-mam-apps-android.md).

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Inicio de sesión único en aplicaciones web conectadas a Azure AD en exploradores protegidos por directivas

Edge para iOS y Android puede aprovechar el inicio de sesión único (SSO) en todas las aplicaciones web (SaaS y locales) que estén conectadas a Azure AD. Con el inicio de sesión único, los usuarios pueden acceder a aplicaciones web conectadas a Azure AD a través de Edge para iOS y Android sin tener que volver a introducir sus credenciales.

Para el inicio de sesión único es necesario que el dispositivo esté registrado con la aplicación Microsoft Authenticator para dispositivos iOS o con el Portal de empresa de Intune en Android. Cuando los usuarios hayan realizado una de estas dos acciones, se les pedirá que registren su dispositivo cuando vayan a una aplicación web conectada a Azure AD en un explorador protegido por directivas (esto solo ocurrirá si su dispositivo no se ha registrado ya). Una vez que el dispositivo esté registrado con la cuenta del usuario administrada por Intune, esa cuenta tendrá el inicio de sesión único habilitado en las aplicaciones web conectadas a Azure AD.

> [!NOTE]
> El registro de dispositivos consiste en un sencillo registro en el servicio de Azure AD. No se requiere una inscripción de dispositivo completa ni se otorga a TI ningún tipo de privilegio extra en el dispositivo.

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>Uso de la configuración de la aplicación para administrar la experiencia de exploración

Edge para iOS y Android admite la configuración de aplicaciones que permiten a los administradores de puntos de conexión unificada, como Microsoft Endpoint Manager, personalizar el comportamiento de la aplicación.

La configuración de aplicaciones se puede entregar a través del canal del sistema operativo de administración de dispositivos móviles (MDM) en los dispositivos inscritos (canal [Configuración de aplicaciones administradas](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) para iOS o canal [Android empresarial](https://developer.android.com/work/managed-configurations) para Android) o a través del canal Directiva de protección de aplicaciones (APP) de Intune. Edge para iOS y Android admite los siguientes escenarios de configuración:

- Permitir solo cuentas profesionales o educativas
- Opciones generales de configuración de aplicaciones
- Configuración de la protección de datos

> [!IMPORTANT]
> En el caso de escenarios de configuración que obligan a la inscripción de dispositivos en Android, los dispositivos deben inscribirse en Android Enterprise y Edge para Android debe implementarse a través del almacén de Google Play administrado. Para obtener más información, vea [Configuración de la inscripción de dispositivos del perfil de trabajo de Android Enterprise](../enrollment/android-work-profile-enroll.md) y [Adición de directivas de configuración de aplicaciones para dispositivos Android Enterprise administrados](app-configuration-policies-use-android.md).

En cada escenario de configuración se indican sus requisitos específicos. Por ejemplo, se especifica si el escenario de configuración necesita la inscripción del dispositivo y, por tanto, funciona con cualquier proveedor de UEM, o bien si necesita directivas de protección de aplicaciones de Intune.

> [!NOTE]
> Con Microsoft Endpoint Manager, la configuración de aplicaciones que se entrega a través del canal del sistema operativo de MDM se conoce como Directiva de configuración de aplicaciones (ACP) de **Dispositivos administrados**, mientras que la configuración de aplicaciones que se entrega a través del canal Directiva de protección de aplicaciones se denomina Directiva de configuración de aplicaciones de **Aplicaciones administradas**.

## <a name="only-allow-work-or-school-accounts"></a>Permitir solo cuentas profesionales o educativas

Respetar las directivas de seguridad y cumplimiento de datos de nuestros clientes más grandes y regulados es un pilar clave del valor de Microsoft 365. Algunas empresas tienen el requisito de capturar toda la información de comunicaciones dentro de su entorno corporativo, así como de asegurarse de que los dispositivos solo se usen para las comunicaciones corporativas. Para admitir estos requisitos, se puede configurar Edge para iOS y Android en dispositivos inscritos para permitir que solo se pueda aprovisionar ahí una cuenta corporativa.

Puede obtener más información sobre la configuración del modo de cuentas permitido por la organización aquí:

- [Configuración de Android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [Configuración de iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Este escenario de configuración solo funciona con dispositivos inscritos. Aun así, se admite cualquier proveedor de UEM. Si no usa Microsoft Endpoint Manager, debe consultar la documentación de UEM para obtener información sobre cómo implementar estas claves de configuración.

## <a name="general-app-configuration-scenarios"></a>Escenarios generales de configuración de aplicaciones

Edge para iOS y Android ofrece a los administradores la posibilidad de personalizar la configuración predeterminada para varias configuraciones de aplicación. Esta función solo se ofrece actualmente cuando Edge para iOS y Android tiene una directiva de protección de aplicaciones de Intune establecida en la cuenta profesional o educativa en la que se ha iniciado sesión en la aplicación.

> [!IMPORTANT]
> Edge para Android no es compatible con la configuración de Chromium disponible en Google Play administrado.

Edge admite los siguientes valores de configuración:

- Experiencias de página Nueva pestaña
- Experiencias de marcador
- Experiencias de comportamiento de la aplicación
- Experiencias de pantalla completa

Estos valores se pueden implementar en la aplicación independientemente del estado de inscripción del dispositivo.

### <a name="new-tab-page-experiences"></a>Experiencias de página Nueva pestaña

Edge para iOS y Android ofrece a las organizaciones varias opciones para ajustar la experiencia de página Nueva pestaña.

#### <a name="organization-logo-and-brand-color"></a>Logotipo y color de marca de la organización

Esta configuración permite personalizar la página Nueva pestaña para Edge para iOS y Android, a fin de que muestre el logotipo y el color de marca de la organización como fondo de la página.

Para cargar el logotipo y el color de la organización, complete primero los siguientes pasos:
1. En [Microsoft Endpoint Manager](https://endpoint.microsoft.com), vaya a **Administración de inquilinos** -> **Personalización** -> **Personalización de marca de identidad de empresa**.
2. Para establecer el logotipo de la marca, junto a **Mostrar en encabezado**, elija "Solo el logotipo de la organización". Se recomienda usar logotipos con un fondo transparente.
3. Para establecer el color de fondo de la marca, seleccione un **Color de tema**. Edge para iOS y Android aplica una sombra más clara del color en la página Nueva pestaña, lo que garantiza que la página tenga una gran legibilidad.

Después, use los siguientes pares clave-valor para extraer la marca de la organización en Edge para iOS y Android:

|    Key    |    Valor    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    **true** muestra el logotipo de marca de la organización.<br>**false** (valor predeterminado) no expone ningún logotipo.    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    **true** muestra el color de marca de la organización.<br>**false** (valor predeterminado) no expondrá ningún color.    |

#### <a name="homepage-shortcut"></a>Acceso directo a la página principal

Esta opción de configuración permite configurar un acceso directo a Edge para iOS y Android en la página principal. El acceso directo que configure en la página principal aparecerá como el primer icono debajo de la barra de búsqueda cuando el usuario abra una nueva pestaña en Edge para iOS y Android. El usuario no puede editar ni eliminar este acceso directo en su contexto administrado. El acceso directo a la página principal muestra el nombre de la organización para distinguirla. 

|    Key    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Especifique una dirección URL válida. Las direcciones URL incorrectas se bloquean como medida de seguridad.<br>Por ejemplo: `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>Varios accesos directos a sitios principales

De forma similar a la configuración de un acceso directo a la página principal, puede configurar varios accesos directos a sitios principales en páginas Nueva pestaña en Edge para iOS y Android. El usuario no puede editar ni eliminar estos accesos directos en un contexto administrado. Nota: Puede configurar un total de ocho accesos directos, incluido un acceso directo a la página principal. Si ha configurado un acceso directo a la página principal, se invalidará el primer sitio principal configurado. 

|    Key    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    Especifique el conjunto de direcciones URL de valor. Cada acceso directo de sitio principal consta de un título y una dirección URL. Separe el título y la dirección URL con el carácter `|`.<br>Por ejemplo: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>Noticias del sector

Puede configurar la experiencia de página Nueva pestaña en Edge para iOS y Android de modo que muestre noticias del sector importantes para su organización. Cuando se habilita esta característica, Edge para iOS y Android usa el nombre de dominio de la organización para agregar noticias de la web sobre la organización, el sector de la organización y la competencia, de modo que los usuarios puedan encontrar noticias externas importantes desde las páginas Nueva pestaña centralizadas de Edge para iOS y Android. Las noticias del sector están desactivadas de forma predeterminada. 

|    Key    |    Valor    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **true** muestra noticias del sector en la página Nueva pestaña.<br>**false** (valor predeterminado) oculta las noticias del sector en la página Nueva pestaña.    |

### <a name="bookmark-experiences"></a>Experiencias de marcador

Edge para iOS y Android ofrece a las organizaciones varias opciones para administrar marcadores.

#### <a name="managed-bookmarks"></a>Marcadores administrados

Para facilitar el acceso, puede configurar los marcadores que quiera que los usuarios tengan disponibles cuando usen Edge para iOS y Android.

- Los marcadores solo aparecen en la cuenta profesional o educativa y no se exponen a las cuentas personales.
- Los usuarios no pueden eliminar ni modificar los marcadores.
- Los marcadores aparecen en la parte superior de la lista. Los marcadores creados por los usuarios aparecen debajo de estos marcadores.
- Si ha habilitado el redireccionamiento del proxy de aplicación, puede agregar aplicaciones web de proxy de aplicación mediante su dirección URL interna o externa.
- Asegúrese de anteponer **http://** o **https://** a todas las direcciones URL al introducirlas en la lista.
- Los marcadores se crean en una carpeta con el nombre de la organización, que se define en Azure Active Directory.

|    Key    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    El valor de esta configuración es una lista de marcadores. Cada marcador consta del título y de la URL del marcador. Separe el título y la dirección URL con el carácter `|`.<br> Por ejemplo: `Microsoft Bing|https://www.bing.com`<p>Para configurar varios marcadores, separe cada par con el carácter doble `||`.<br>Por ejemplo:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>Marcador Mis aplicaciones

De forma predeterminada, los usuarios tienen el marcador Mis aplicaciones configurado dentro de la carpeta de la organización en Edge para iOS y Android.

|    Key    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **true** (valor predeterminado) muestra Mis aplicaciones en los marcadores de Edge para iOS y Android.<br>**false** oculta Mis aplicaciones en Edge para iOS y Android.    |

### <a name="app-behavior-experiences"></a>Experiencias de comportamiento de la aplicación

Edge para iOS y Android ofrece a las organizaciones varias opciones para administrar el comportamiento de la aplicación.

#### <a name="default-protocol-handler"></a>Controlador del protocolo predeterminado

De forma predeterminada, Edge para iOS y Android usa el controlador de protocolo HTTPS cuando el usuario no especifica el protocolo en la dirección URL. Por lo general, esto se considera un procedimiento recomendado. pero puede deshabilitarse.

|    Key    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     **true** (valor predeterminado) indica que el controlador de protocolo predeterminado es HTTPS.<br>**false** indica que el controlador de protocolo predeterminado es HTTP.     |

#### <a name="disable-data-sharing-for-personalization"></a>Deshabilitación del uso compartido de datos para la personalización

De forma predeterminada, Edge para iOS y Android solicita a los usuarios la recopilación de datos de uso y el uso compartido del historial de exploración para personalizar la experiencia de exploración. Las organizaciones pueden deshabilitar el uso compartido de estos datos si impiden que se muestre este aviso a los usuarios finales.

|    Key    |    Valor    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     **true** deshabilita que se muestre esta solicitud a los usuarios finales.<br>**false** (valor predeterminado) indica que se pide a los usuarios que compartan los datos de uso.    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     **true** deshabilita que se muestre esta solicitud a los usuarios finales.<br>**false** (valor predeterminado) indica que se pide a los usuarios que compartan el historial de exploración.     |

#### <a name="disable-specific-features"></a>Deshabilitación de características específicas

Edge para iOS y Android permite a las organizaciones deshabilitar determinadas características que están habilitadas de forma predeterminada. Para deshabilitar dichas características, establezca la siguiente configuración:

|    Key    |    Valor    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    **password** deshabilita los mensajes que ofrecen la posibilidad de guardar contraseñas para el usuario final.<br>**inprivate** deshabilita la exploración InPrivate.<p>Para deshabilitar varias características, separe los valores con `|`. Por ejemplo, `inprivate|password` deshabilita tanto InPrivate como el almacenamiento de contraseñas.     |

> [!NOTE]
> Edge para Android no permite deshabilitar el administrador de contraseñas.

#### <a name="disable-extensions"></a>Deshabilitación de extensiones

Puede deshabilitar el marco de extensiones en Edge para Android con el fin de impedir que los usuarios instalen extensiones de aplicaciones. Para ello, establezca la siguiente configuración:

|    Key    |    Valor    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    **true** deshabilita el marco de extensiones.<br>**false** (valor predeterminado) habilita el marco de extensiones.    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Experiencias de pantalla completa en dispositivos Android

Edge para Android se puede habilitar como aplicación de pantalla completa con la siguiente configuración:

|    Key    |    Valor    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    **true** habilita la pantalla completa en Edge para Android.<br>**false** (valor predeterminado) deshabilita la pantalla completa.    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    **true** muestra la barra de direcciones en pantalla completa.<br> **false** (valor predeterminado) oculta la barra de direcciones en pantalla completa.    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    **true** muestra la barra de acciones inferior en pantalla completa.<br> **false** (valor predeterminado) oculta la barra inferior en pantalla completa.    |

## <a name="data-protection-app-configuration-scenarios"></a>Escenarios de configuración de aplicaciones de protección de datos

Edge para iOS y Android admite directivas de configuración de aplicaciones para la siguiente configuración de protección de datos cuando la aplicación se administra mediante Microsoft Endpoint Manager con una directiva de protección de aplicaciones de Intune aplicada a la cuenta profesional o educativa en la que se ha iniciado sesión en la aplicación:

- Administración de la sincronización de cuentas
- Administración de sitios web restringidos
- Administración de la configuración del proxy
- Administración de sitios de inicio de sesión único NTLM

Estos valores se pueden implementar en la aplicación independientemente del estado de inscripción del dispositivo.

### <a name="manage-account-synchronization"></a>Administración de la sincronización de cuentas

De forma predeterminada, la sincronización de Microsoft Edge permite a los usuarios acceder a los datos de exploración en todos sus dispositivos con sesión iniciada. Los datos que admite la sincronización incluyen los siguientes:

- Favoritos
- Contraseñas
- Direcciones y más (entrada de formulario de autorrelleno)

La función de sincronización se habilita mediante el consentimiento del usuario y los usuarios pueden activar o desactivar la sincronización para cada uno de los tipos de datos enumerados anteriormente. Para obtener más información, vea [Sincronización de Microsoft Edge](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync).

Las organizaciones tienen la capacidad de deshabilitar la sincronización de Edge en iOS y Android. 

|Key  |Valor  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |**true** (valor predeterminado) permite la sincronización de Edge.<br>**false** deshabilita la sincronización de Edge.          |

### <a name="manage-restricted-web-sites"></a>Administración de sitios web restringidos

Las organizaciones pueden definir a qué sitios pueden acceder los usuarios dentro del contexto de la cuenta profesional o educativa en Edge para iOS y Android. Si usa una lista de permitidos, los usuarios solo podrán acceder a los sitios que se hayan indicado explícitamente. Si usa una lista de bloqueados, los usuarios podrán acceder a todos los sitios excepto los que haya bloqueado explícitamente. Solo puede imponer una lista de permitidos o bien una de bloqueados, pero no ambas a la vez. Si se imponen ambas, solo se admitirá la lista de permitidos.

La organización también define lo que ocurre cuando un usuario intenta navegar a un sitio web restringido. De forma predeterminada, se permiten las transiciones. Si la organización lo permite, los sitios web restringidos pueden abrirse en el contexto de la cuenta personal, en el contexto de InPrivate de la cuenta de Azure AD o si el sitio está completamente bloqueado. Para obtener más información sobre los distintos escenarios que se admiten, vea [Transiciones de sitios web restringidos en Microsoft Edge para dispositivos móviles](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333). Al permitir las experiencias de transición, los usuarios de la organización permanecen protegidos y, al mismo tiempo, los recursos corporativos se mantienen seguros.

> [!NOTE]
> Edge para iOS y Android puede bloquear el acceso a sitios solo cuando se accede a estos directamente. No bloquea el acceso cuando los usuarios usan servicios intermedios (por ejemplo, un servicio de traducción) para acceder al sitio.

Use los siguientes pares clave-valor para configurar una lista de sitios permitidos o bloqueados para Edge para iOS y Android. 

|Key  |Valor  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |El valor correspondiente de la clave es una lista de direcciones URL. Escriba todas las direcciones URL que quiera permitir como un valor único, separadas por un carácter de barra vertical `|`.<p>**Ejemplos:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |El valor correspondiente de la clave es una lista de direcciones URL. Escriba todas las direcciones URL que quiera bloquear como un valor único, separadas por un carácter de barra vertical `|`.<br>**Ejemplos:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |**true** (valor predeterminado) permite que Edge para iOS y Android realice la transición a sitios restringidos. Cuando no se deshabilitan las cuentas personales, se pide a los usuarios que cambien al contexto personal para abrir el sitio restringido o bien que agreguen una cuenta personal. Si com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked se establece en true, los usuarios pueden abrir el sitio restringido en el contexto de InPrivate.<p>**false** impide que Edge para iOS y Android realice la transición de los usuarios. A los usuarios simplemente se les muestra un mensaje en el que se indica que el sitio al que intentan acceder está bloqueado.         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |**true** permite abrir sitios restringidos en el contexto de InPrivate de la cuenta de Azure AD. Si la cuenta de Azure AD es la única configurada en Edge para iOS y Android, el sitio restringido se abre automáticamente en el contexto de InPrivate. Si el usuario tiene configurada una cuenta personal, se le pedirá que elija entre abrir InPrivate o cambiar a la cuenta personal.<p> **false** (valor predeterminado) requiere que el sitio restringido se abra en la cuenta personal del usuario. Si las cuentas personales están deshabilitadas, el sitio se bloquea.<p>Para que esta configuración surta efecto, com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock debe establecerse en true.          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | Escriba el número de segundos que los usuarios verán la notificación de la barra emergente "Vínculo abierto con el modo InPrivate. La organización requiere el uso del modo InPrivate para este contenido". De forma predeterminada, la notificación de la barra emergente se muestra durante siete segundos.

Siempre se permiten los siguientes sitios con independencia de la configuración definida para la lista de permitidos o la lista de bloqueados:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>Formatos de URL para la lista de sitios permitidos y bloqueados 

Puede usar diferentes formatos de URL para crear listas de sitios permitidos o bloqueados. Estos patrones permitidos se detallan en la tabla siguiente.

- Asegúrese de anteponer **http://** o **https://** a todas las direcciones URL al introducirlas en la lista.
- Puede usar el carácter comodín (\*) según las reglas de la siguiente lista de patrones permitidos.
- Un carácter comodín solo puede coincidir con un componente entero del nombre de host (separado por puntos) o partes completas de la ruta de acceso (separadas por barras diagonales). Por ejemplo, `http://*contoso.com`**no** es compatible.
- Puede especificar números de puerto en la dirección. Si no especifica un número de puerto, los valores usados son:
  - Puerto 80 para http
  - Puerto 443 para https
- **No** se admite el uso de caracteres comodín para el número de puerto. Por ejemplo, `http://www.contoso.com:*` y `http://www.contoso.com:*/` no se admiten. 

    |    Dirección URL    |    Detalles    |    Coincide    |    No coincide    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Coincide con una sola página    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Coincide con una sola página    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    Coincide con todas las direcciones URL que comienzan por `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Coincide con todos los subdominios en `contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Coincide con todos los subdominios que terminan en `contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    Coincide con una sola carpeta    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Coincide con una sola página, con un número de puerto    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Coincide con una sola página segura    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Coincide con una sola carpeta y todas sus subcarpetas    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Los siguientes son ejemplos de algunas de las entradas que no se pueden especificar:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - Direcciones IP
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>Administración de la configuración del proxy

Puede usar Edge para iOS y Android junto con [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) para proporcionar a los usuarios acceso a sitios de la intranet desde sus dispositivos móviles. Por ejemplo: 

- Un usuario está utilizando la aplicación móvil de Outlook, que está protegida por Intune. El usuario hace clic en un vínculo de un correo electrónico que dirige a un sitio de la intranet y Edge para iOS y Android reconoce que dicho sitio se ha expuesto al usuario a través del proxy de aplicación. El usuario se enruta automáticamente a través del proxy de aplicación para que se autentique con una autenticación multifactor y un acceso condicional antes de llegar al sitio de la intranet. Ahora el usuario puede acceder a sitios internos incluso desde sus dispositivos móviles y el vínculo de Outlook funciona según lo previsto.
- Un usuario abre Edge para iOS y Android en su dispositivo iOS o Android. Si Edge para iOS y Android está protegido con Intune y el proxy de aplicación está habilitado, el usuario puede ir a un sitio de la intranet mediante la URL interna como de costumbre. Edge para iOS y Android reconoce que este sitio de intranet se ha expuesto al usuario a través del proxy de aplicación. El usuario se enruta automáticamente a través del proxy de aplicación para autenticarse antes de llegar al sitio de la intranet. 

Antes de empezar:

- Configure las aplicaciones internas a través de Azure AD Application Proxy.
  - Para configurar el proxy de aplicación y publicar aplicaciones, vea la [documentación de configuración](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).
- La aplicación de Edge para iOS y Android debe tener una [directiva de protección de aplicaciones de Intune](app-protection-policy.md) asignada.
- Las aplicaciones de Microsoft deben contar con una directiva de protección de aplicaciones que tenga el valor de configuración de transferencia de datos **Restringir la transferencia de contenido web con otras aplicaciones** establecido en **Microsoft Edge**.

> [!NOTE]
> Los datos de redireccionamiento actualizados del proxy de aplicación pueden tardar hasta 24 horas en aplicarse en Edge para iOS y Android.

Establezca como destino Edge para iOS con el siguiente par clave-valor a fin de habilitar el proxy de aplicación:

|    Key    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **true** habilita escenarios de redirección del proxy de aplicación de Azure AD.<br>**false** (valor predeterminado) impide los escenarios del proxy de aplicación de Azure AD.    |

> [!NOTE]
> Edge para Android no usa esta clave. En su lugar, Edge para Android consume automáticamente la configuración del proxy de aplicación de Azure AD, siempre y cuando la cuenta de Azure AD en la que se ha iniciado sesión tenga aplicada una directiva de protección de aplicaciones.

Para obtener más información sobre cómo usar Edge para iOS y Android y Azure AD Application Proxy conjuntamente para acceder sin problemas (y de forma segura) a las aplicaciones web locales, vea [Better together: Intune and Azure Active Directory team up to improve user access](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254) (Juntos mejor: Intune y Azure Active Directory unen fuerzas para mejorar el acceso de usuario). En esta entrada de blog se hace referencia a Intune Managed Browser, pero el contenido también se aplica a Edge para iOS y Android.

### <a name="manage-ntlm-single-sign-on-sites"></a>Administración de sitios de inicio de sesión único NTLM

Las organizaciones pueden obligar a los usuarios a autenticarse con NTLM para acceder a sitios web de la intranet. De forma predeterminada, se pide a los usuarios que escriban las credenciales cada vez que acceden a un sitio web que requiere la autenticación NTLM, ya que el almacenamiento en caché de credenciales NTLM está deshabilitado. 

Las organizaciones pueden habilitar el almacenamiento en caché de credenciales NTLM para sitios web concretos. Para estos sitios, después de que el usuario escriba las credenciales y se autentique correctamente, las credenciales se almacenan en caché de forma predeterminada durante 30 días.


|Key  |Valor  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |El valor correspondiente de la clave es una lista de direcciones URL. Escriba todas las direcciones URL que quiera permitir como un valor único, separadas por un carácter de barra vertical `|`.<p>**Ejemplos:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>Para obtener más información sobre los tipos de formato de dirección URL que se admiten, vea [Formatos de URL para la lista de sitios permitidos y bloqueados](#url-formats-for-allowed-and-blocked-site-list).         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |Número de horas para almacenar en caché las credenciales. El valor predeterminado es de 720 horas.         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Implementación de escenarios de configuración de aplicaciones con Microsoft Endpoint Manager

Si usa Microsoft Endpoint Manager como proveedor de administración de aplicaciones móviles, los siguientes pasos le permiten crear una directiva de configuración de aplicaciones administradas. Una vez creada la configuración, puede asignar sus valores a grupos de usuarios.

1. Inicie sesión en [Microsoft Endpoint Manager](https://endpoint.microsoft.com).

2. Seleccione **Aplicaciones** y **Directivas de configuración de aplicaciones**.

3. En la hoja **Directivas de configuración de aplicaciones**, elija **Agregar** y **Aplicaciones administradas**.

4. En la sección **Conceptos básicos**, escriba un **nombre** y una **descripción** opcional para las opciones de configuración de aplicaciones.

5. En **Aplicaciones públicas**, elija **Seleccionar aplicaciones públicas**. En la hoja **Aplicaciones de destino**, seleccione las aplicaciones de la plataforma iOS y Android para elegir **Edge para iOS y Android**. Haga clic en **Seleccionar** para guardar las aplicaciones públicas seleccionadas.

6. Haga clic en **Siguiente** para completar la configuración básica de la directiva de configuración de aplicaciones.

7. En la sección **Configuración**, expanda los **Valores de configuración de Edge**.

8. Si quiere administrar la configuración de protección de datos, establezca las opciones deseadas según corresponda:

    - Para **Redirección de proxy de aplicación**, elija entre las opciones disponibles: **Habilitar** o **Deshabilitar** (valor predeterminado).

    - Para **Dirección URL de acceso directo a la página principal**, especifique una dirección URL válida que incluya el prefijo *http://* o *https://* . Las direcciones URL incorrectas se bloquean como medida de seguridad.

    - Para **Marcadores administrados**, especifique una dirección URL válida que incluya el prefijo *http://* o *https://* .

    - Para **Direcciones URL permitidas**, especifique una dirección URL válida (solo se permiten estas direcciones URL; no se puede acceder a ningún otro sitio). Para obtener más información sobre los tipos de formato de dirección URL que se admiten, vea [Formatos de URL para la lista de sitios permitidos y bloqueados](#url-formats-for-allowed-and-blocked-site-list).

    - Para **Direcciones URL bloqueadas**, especifique una dirección URL válida (solo se bloquean estas direcciones URL). Para obtener más información sobre los tipos de formato de dirección URL que se admiten, vea [Formatos de URL para la lista de sitios permitidos y bloqueados](#url-formats-for-allowed-and-blocked-site-list).

    - En **Redirigir los sitios restringidos a un contexto personal**, elija entre las opciones disponibles: **Habilitar** (valor predeterminado) o **Deshabilitar**.

    > [!NOTE]
    > Cuando se definen las direcciones URL permitidas y las direcciones URL bloqueadas en la directiva, solo se admite la lista de permitidos.

9. Si quiere que las opciones de configuración adicionales de la aplicación no se expongan en la directiva anterior, expanda el nodo **Opciones de configuración generales** y especifique como corresponda los pares clave-valor.

10. Cuando haya terminado de configurar la programación, seleccione **Siguiente**.

11. En la sección **Asignaciones**, elija **Seleccionar grupos para incluir**. Seleccione el grupo de Azure AD al que quiere asignar la directiva de configuración de aplicación y elija **Seleccionar**.

12. Cuando haya terminado con las asignaciones, elija **Siguiente**.

13. En la hoja **Crear una directiva de configuración de aplicaciones**, revise la configuración establecida y elija **Crear**.

La directiva de configuración recién creada se muestra en la hoja **Configuración de la aplicación**.

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>Uso de Edge para iOS y Android para acceder a registros de aplicaciones administradas

Los usuarios que tengan instalado Edge para iOS y Android en el dispositivo iOS o Android pueden ver el estado de administración de todas las aplicaciones publicadas de Microsoft. Pueden enviar registros para solucionar problemas de sus aplicaciones iOS o Android administradas mediante los pasos siguientes:

1. Abra Edge para iOS y Android en el dispositivo.
2. Escriba `about:intunehelp` en el cuadro de dirección.
3. Edge para iOS y Android inicia el modo de solución de problemas.

Para obtener una lista de las opciones de configuración almacenadas en los registros de la aplicación, vea [Revisión de los registros de protección de aplicaciones cliente](app-protection-policy-settings-log.md).

Para ver cómo se pueden consultar los registros en dispositivos Android, vea [Enviar registros al administrador de TI por correo electrónico](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android).

## <a name="next-steps"></a>Pasos siguientes

- [¿Qué son las directivas de protección de aplicaciones?](app-protection-policy.md) 
- [Directivas de configuración de aplicaciones para Microsoft Intune](app-configuration-policies-overview.md)