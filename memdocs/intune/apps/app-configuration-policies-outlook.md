---
title: Administración de Outlook para iOS y Android con Intune
description: Use las directivas de configuración y protección de aplicaciones de Intune con Outlook para iOS y Android a fin de garantizar que siempre se apliquen medidas de seguridad al acceder a experiencias de colaboración en equipo.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3db207e4c1c75706c1f54762bf74c1757d342ac1
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973050"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>Administración del acceso de colaboración a través de mensajería mediante Outlook para iOS y Android con Microsoft Intune

La aplicación Outlook para iOS y Android está diseñada para permitir que los usuarios de la organización saquen un mayor provecho de los dispositivos móviles, ya que integra el correo electrónico, el calendario, los contactos y otros archivos.

Tendrá a su disposición las capacidades de protección más enriquecidas y más amplias para los datos de Office 365 cuando se suscriba al conjunto de aplicaciones de Enterprise Mobility + Security, que incluye características de Microsoft Intune y Azure Active Directory Premium, como el acceso condicional. Como mínimo, le interesará implementar una directiva de acceso condicional que permita la conectividad a Outlook para iOS y Android desde dispositivos móviles y una directiva de protección de aplicaciones de Intune que garantice que la experiencia de colaboración esté protegida.

## <a name="apply-conditional-access"></a>Aplicación del acceso condicional
Las organizaciones pueden usar directivas de acceso condicional de Azure AD para asegurarse de que los usuarios solo puedan acceder al contenido profesional o educativo mediante Outlook para iOS y Android. Para ello, necesitará una directiva de acceso condicional destinada a todos los usuarios potenciales. Encontrará más información sobre la creación de esta directiva en [Uso obligatorio de directivas de protección de aplicaciones para el acceso a aplicaciones en la nube con acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Siga el "Paso 1: Configuración de una directiva de acceso condicional de Azure AD para Office 365" del [Escenario 1: Las aplicaciones de Office 365 requieren aplicaciones aprobadas con directivas de protección de aplicaciones](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), que permite Outlook para iOS y Android, pero impide que los clientes de Exchange ActiveSync compatibles con OAuth se conecten a Exchange Online.

   > [!NOTE]
   > Esta directiva garantiza que los usuarios móviles puedan acceder a todos los puntos de conexión de Office mediante las aplicaciones correspondientes.

2. Siga el "Paso 2: Configuración de una directiva de acceso condicional de Azure AD para Exchange Online con ActiveSync (EAS)" del [Escenario 1: Las aplicaciones de Office 365 requieren aplicaciones aprobadas con directivas de protección de aplicaciones](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), que impide que los clientes de Exchange ActiveSync que aprovechan la autenticación básica se conecten a Exchange Online.

   Las directivas anteriores aprovechan el control de concesión [Requerir directiva de protección de aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference), lo que garantiza que se aplique una directiva de Intune App Protection a la cuenta asociada en Outlook para iOS y Android antes de conceder acceso. Si el usuario no está asignado a una directiva de Intune App Protection, no tiene licencia para Intune o la aplicación no está incluida en la directiva de Intune App Protection, la directiva impide que el usuario obtenga un token de acceso y pueda acceder a los datos de mensajería.

3. Por último, siga el [Procedimiento: Bloqueo de la autenticación heredada en Azure AD con acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/block-legacy-authentication) para bloquear la autenticación heredada para otros protocolos de Exchange en dispositivos iOS y Android. Esta directiva debe tener como destino solo la aplicación en la nube de Office 365 Exchange Online y las plataformas de dispositivos iOS y Android. Esto garantiza que las aplicaciones móviles que usan los protocolos de servicios web de Exchange, IMAP4 o POP3 con autenticación básica no puedan conectarse a Exchange Online.

## <a name="create-intune-app-protection-policies"></a>Creación de directivas de protección de aplicaciones de Intune

Las directivas de protección de aplicaciones (APP) definen qué aplicaciones están permitidas y qué acciones pueden llevar a cabo con los datos de la organización. Las opciones disponibles en APP permiten a las organizaciones adaptar la protección a sus necesidades específicas. Para algunas de ellas, puede que no sea obvio qué configuración de directivas es necesaria para implementar un escenario completo. Para ayudar a las organizaciones a priorizar la protección del punto de conexión del cliente móvil, Microsoft ha introducido la taxonomía para su marco de protección de datos de APP para la administración de aplicaciones móviles de iOS y Android.

El marco de protección de datos de APP se organiza en tres niveles de configuración distintos, cada uno de ellos basado en el nivel anterior:

- La **protección de datos empresariales básica** (nivel 1) garantiza que las aplicaciones estén protegidas con un PIN y cifradas, y realiza operaciones de borrado selectivo. En el caso de los dispositivos Android, este nivel valida la certificación de dispositivos Android. Se trata de una configuración de nivel de entrada que proporciona un control de protección de datos similar en las directivas de buzón de Exchange Online y que introduce tecnologías informáticas y el rellenado de usuarios en APP.
- La **protección de datos empresariales mejorada** (nivel 2) incorpora mecanismos para la prevención de la pérdida de datos de APP y requisitos mínimos para el sistema operativo. Esta es la configuración aplicable a la mayoría de los usuarios móviles que acceden a datos profesionales o educativos.
- La **protección de datos empresariales alta** (nivel 3) incorpora mecanismos avanzados para la protección de datos, configuración de PIN mejorada y defensa contra amenazas móviles de APP. Esta configuración es conveniente para los usuarios que acceden a datos de alto riesgo.

Para ver las recomendaciones específicas para cada nivel de configuración y las aplicaciones mínimas que se deben proteger, revise el [Marco de protección de datos mediante directivas de protección de aplicaciones](app-protection-framework.md).

Independientemente de si el dispositivo está inscrito en una solución de administración de puntos de conexión unificada (UEM), es necesario crear una directiva de protección de aplicaciones de Intune para las aplicaciones iOS y Android con los pasos descritos en [Creación y asignación de directivas de protección de aplicaciones](app-protection-policies.md). Estas directivas deben cumplir como mínimo las siguientes condiciones:

1. Incluir todas las aplicaciones para dispositivos móviles de Microsoft 365, como Edge, Outlook, OneDrive, Office o Teams, ya que esto garantizará que los usuarios puedan acceder a los datos profesionales o educativos y manipularlos desde cualquier aplicación de Microsoft de forma segura.

2. Deben asignarse a todos los usuarios. Esto garantiza que todos los usuarios estén protegidos, independientemente de si usan Outlook para iOS o Android.

3. Deben determinar qué nivel de marco cumple los requisitos. La mayoría de las organizaciones deben implementar la configuración definida en la **protección de datos empresariales mejorada** (nivel 2), ya que habilita los controles de protección de datos y de requisitos de acceso.

Para obtener más información sobre las configuraciones disponibles, vea [Configuración de directivas de protección de aplicaciones Android](app-protection-policy-settings-android.md) y [Configuración de directivas de protección de aplicaciones iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Para aplicar directivas de protección de aplicaciones de Intune a aplicaciones en dispositivos Android que no están inscritos en Intune, el usuario también debe instalar el Portal de empresa de Intune. Para obtener más información, vea [Qué esperar cuando la aplicación Android está administrada por directivas de protección de aplicaciones](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Uso de la configuración de aplicaciones

Outlook para iOS y Android admite la configuración de aplicaciones que permite a los administradores de puntos de conexión unificada, como Microsoft Endpoint Manager, personalizar el comportamiento de la aplicación.

La configuración de aplicaciones se puede entregar a través del canal del sistema operativo de administración de dispositivos móviles (MDM) en los dispositivos inscritos (canal [Configuración de aplicaciones administradas](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) para iOS o canal [Android empresarial](https://developer.android.com/work/managed-configurations) para Android) o a través del canal Directiva de protección de aplicaciones (APP) de Intune. Outlook para iOS y Android admite los siguientes escenarios de configuración:

- Permitir solo cuentas profesionales o educativas
- Opciones generales de configuración de aplicaciones
- Configuración de S/MIME
- Configuración de la protección de datos

Para ver los pasos concretos del procedimiento y la documentación detallada sobre las opciones de configuración de aplicaciones que admite Outlook en iOS y Android, vea [Implementación de opciones de configuración de Outlook para aplicaciones iOS y Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="next-steps"></a>Pasos siguientes

- [¿Qué son las directivas de protección de aplicaciones?](app-protection-policy.md) 
- [Directivas de configuración de aplicaciones para Microsoft Intune](app-configuration-policies-overview.md)