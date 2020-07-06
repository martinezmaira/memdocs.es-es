---
title: Administración de Office para iOS y Android con Intune
titleSuffix: ''
description: Use las directivas de configuración y protección de aplicaciones de Intune con Office para iOS y Android a fin de garantizar que siempre se apliquen medidas de seguridad al acceder a experiencias de colaboración.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d23eaeee839122bad46cd9619a790b9ca6332a6
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383264"
---
# <a name="manage-collaboration-experiences-using-office-for-ios-and-android-with-microsoft-intune"></a>Administración de experiencias de colaboración mediante Office para iOS y Android con Microsoft Intune

Office para iOS y Android ofrece varias ventajas clave, entre las que se incluyen las siguientes:

- Combina Word, Excel y PowerPoint de una forma que simplifica la experiencia, con menos aplicaciones para descargar o entre las que cambiar. Requiere mucho menos almacenamiento en el teléfono que la instalación de aplicaciones individuales, a la vez que mantiene prácticamente todas las funciones de las aplicaciones móviles existentes que los usuarios ya conocen y emplean.
- Integra la tecnología Office Lens para desbloquear la potencia de la cámara con funciones como la conversión de imágenes en documentos de Word y Excel editables, el examen de archivos PDF y la captura de pizarras con mejoras digitales automáticas para facilitar la lectura del contenido.
- Agrega nuevas funciones a las tareas comunes que suelen llevar a cabo los usuarios al trabajar en un teléfono, como tomar notas rápidas, firmar archivos PDF, escanear códigos QR y transferir archivos entre dispositivos.

Tendrá a su disposición las capacidades de protección más enriquecidas y más amplias para los datos de Office 365 cuando se suscriba al conjunto de aplicaciones de Enterprise Mobility + Security, que incluye características de Microsoft Intune y Azure Active Directory Premium, como el acceso condicional. Como mínimo, le interesará implementar una directiva de acceso condicional que permita la conectividad a Office para iOS y Android desde dispositivos móviles y una directiva de protección de aplicaciones de Intune que garantice que la experiencia de colaboración esté protegida.

## <a name="apply-conditional-access"></a>Aplicación del acceso condicional
Las organizaciones pueden usar directivas de acceso condicional de Azure AD para asegurarse de que los usuarios solo puedan acceder al contenido profesional o educativo mediante Office para iOS y Android. Para ello, necesitará una directiva de acceso condicional destinada a todos los usuarios potenciales. Encontrará más información sobre la creación de esta directiva en [Uso obligatorio de directivas de protección de aplicaciones para el acceso a aplicaciones en la nube con acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Siga el "Paso 1: Configuración de una directiva de acceso condicional de Azure AD para Office 365" del [Escenario 1: Las aplicaciones de Office 365 requieren aplicaciones aprobadas con directivas de protección de aplicaciones](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), que permite Office para iOS y Android, pero impide que los clientes de dispositivos móviles compatibles con OAuth de terceros se conecten a los puntos de conexión de Office 365.

   >[!NOTE]
   > Esta directiva garantiza que los usuarios móviles puedan acceder a todos los puntos de conexión de Office mediante las aplicaciones correspondientes.

## <a name="create-intune-app-protection-policies"></a>Creación de directivas de protección de aplicaciones de Intune

Las directivas de protección de aplicaciones (APP) definen qué aplicaciones están permitidas y qué acciones pueden llevar a cabo con los datos de la organización. Las opciones disponibles en APP permiten a las organizaciones adaptar la protección a sus necesidades específicas. Para algunas de ellas, puede que no sea obvio qué configuración de directivas es necesaria para implementar un escenario completo. Para ayudar a las organizaciones a priorizar la protección del punto de conexión del cliente móvil, Microsoft ha introducido la taxonomía para su marco de protección de datos de APP para la administración de aplicaciones móviles de iOS y Android.

El marco de protección de datos de APP se organiza en tres niveles de configuración distintos, cada uno de ellos basado en el nivel anterior:

- La **protección de datos empresariales básica** (nivel 1) garantiza que las aplicaciones estén protegidas con un PIN y cifradas, y realiza operaciones de borrado selectivo. En el caso de los dispositivos Android, este nivel valida la certificación de dispositivos Android. Se trata de una configuración de nivel de entrada que proporciona un control de protección de datos similar en las directivas de buzón de Exchange Online y que introduce tecnologías informáticas y el rellenado de usuarios en APP.
- La **protección de datos empresariales mejorada** (nivel 2) incorpora mecanismos para la prevención de la pérdida de datos de APP y requisitos mínimos para el sistema operativo. Esta es la configuración aplicable a la mayoría de los usuarios móviles que acceden a datos profesionales o educativos.
- La **protección de datos empresariales alta** (nivel 3) incorpora mecanismos avanzados para la protección de datos, configuración de PIN mejorada y defensa contra amenazas móviles de APP. Esta configuración es conveniente para los usuarios que acceden a datos de alto riesgo.

Para ver las recomendaciones específicas para cada nivel de configuración y las aplicaciones mínimas que se deben proteger, revise el [Marco de protección de datos mediante directivas de protección de aplicaciones](app-protection-framework.md).

Independientemente de si el dispositivo está inscrito en una solución de administración de puntos de conexión unificada (UEM), es necesario crear una directiva de protección de aplicaciones de Intune para las aplicaciones iOS y Android con los pasos descritos en [Creación y asignación de directivas de protección de aplicaciones](app-protection-policies.md). Estas directivas deben cumplir como mínimo las siguientes condiciones:

1. Deben incluir todas las aplicaciones para dispositivos móviles de Microsoft 365, como Edge, Outlook, OneDrive, Office o Teams, ya que esto garantizará que los usuarios puedan acceder a los datos profesionales o educativos y manipularlos desde cualquier aplicación de Microsoft de forma segura.

2. Deben asignarse a todos los usuarios. Esto garantiza que todos los usuarios estén protegidos, independientemente de si usan Office para iOS o Android.

3. Deben determinar qué nivel de marco cumple los requisitos. La mayoría de las organizaciones deben implementar la configuración definida en la **protección de datos empresariales mejorada** (nivel 2), ya que habilita los controles de protección de datos y de requisitos de acceso.

Para obtener más información sobre las configuraciones disponibles, vea [Configuración de directivas de protección de aplicaciones Android](app-protection-policy-settings-android.md) y [Configuración de directivas de protección de aplicaciones iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Para aplicar directivas de protección de aplicaciones de Intune a aplicaciones en dispositivos Android que no están inscritos en Intune, el usuario también debe instalar el Portal de empresa de Intune. Para obtener más información, vea [Qué esperar cuando la aplicación Android está administrada por directivas de protección de aplicaciones](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Uso de la configuración de aplicaciones

Office para iOS y Android admite la configuración de aplicaciones que permite a los administradores de puntos de conexión unificada, como Microsoft Endpoint Manager, personalizar el comportamiento de la aplicación.

La configuración de aplicaciones se puede entregar a través del canal del sistema operativo de administración de dispositivos móviles (MDM) en los dispositivos inscritos (canal [Configuración de aplicaciones administradas](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) para iOS o canal [Android empresarial](https://developer.android.com/work/managed-configurations) para Android) o a través del canal Directiva de protección de aplicaciones (APP) de Intune. Office para iOS y Android admite los siguientes escenarios de configuración:

- Permitir solo cuentas profesionales o educativas
- Configuración de la protección de datos

> [!IMPORTANT]
> En el caso de escenarios de configuración que obligan a la inscripción de dispositivos en Android, los dispositivos deben inscribirse en Android Enterprise y Office para Android debe implementarse a través del almacén de Google Play administrado. Para obtener más información, vea [Configuración de la inscripción de dispositivos del perfil de trabajo de Android Enterprise](../enrollment/android-work-profile-enroll.md) y [Adición de directivas de configuración de aplicaciones para dispositivos Android Enterprise administrados](app-configuration-policies-use-android.md).

En cada escenario de configuración se indican sus requisitos específicos. Por ejemplo, se especifica si el escenario de configuración necesita la inscripción del dispositivo y, por tanto, funciona con cualquier proveedor de UEM, o bien si necesita directivas de protección de aplicaciones de Intune.

> [!NOTE]
> Con Microsoft Endpoint Manager, la configuración de aplicaciones que se entrega a través del canal del sistema operativo de MDM se conoce como Directiva de configuración de aplicaciones (ACP) de **Dispositivos administrados**, mientras que la configuración de aplicaciones que se entrega a través del canal Directiva de protección de aplicaciones se denomina Directiva de configuración de aplicaciones de **Aplicaciones administradas**.

## <a name="only-allow-work-or-school-accounts"></a>Permitir solo cuentas profesionales o educativas

Respetar las directivas de seguridad y cumplimiento de datos de nuestros clientes más grandes y regulados es un pilar clave del valor de Microsoft 365. Algunas empresas tienen el requisito de capturar toda la información de comunicaciones dentro de su entorno corporativo, así como de asegurarse de que los dispositivos solo se usen para las comunicaciones corporativas. Para admitir estos requisitos, se puede configurar Office para Android en dispositivos inscritos para permitir que solo se pueda aprovisionar en la aplicación una cuenta corporativa.

Puede obtener más información sobre la configuración del modo de cuentas permitido por la organización aquí:

- [Configuración de Android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Este escenario de configuración solo funciona con dispositivos inscritos. Aun así, se admite cualquier proveedor de UEM. Si no usa Microsoft Endpoint Manager, debe consultar la documentación de UEM para obtener información sobre cómo implementar estas claves de configuración.

> [!NOTE]
> En este momento, solo Office para Android admite el modo de cuentas permitido por la organización.

## <a name="data-protection-app-configuration-scenarios"></a>Escenarios de configuración de aplicaciones de protección de datos

Office para iOS y Android admite directivas de configuración de aplicaciones para la siguiente configuración de protección de datos cuando la aplicación se administra mediante Microsoft Endpoint Manager con una directiva de protección de aplicaciones de Intune aplicada a la cuenta profesional o educativa en la que se ha iniciado sesión en la aplicación:

- Administración de transferencias de archivos mediante la acción Transferir archivos
- Administración de transferencias de archivos mediante la acción Compartir cercanos

Estos valores se pueden implementar en la aplicación independientemente del estado de inscripción del dispositivo.

### <a name="manage-file-transfers"></a>Administración de transferencias de archivos

De forma predeterminada, Office para iOS y Android permite a los usuarios compartir contenido mediante diversos mecanismos:

- Si el archivo se hospeda en OneDrive o SharePoint, los usuarios pueden iniciar una solicitud de recurso compartido directamente en el archivo.
- Los usuarios pueden transferir archivos a sistemas de escritorio mediante la acción **Transferir archivos**.
- Los usuarios pueden compartir archivos con dispositivos móviles cercanos mediante la acción **Compartir cercanos**.

Las acciones **Transferir archivos** y **Compartir cercanos** solo funcionan con elementos multimedia, archivos locales y archivos que no están protegidos por una directiva de protección de aplicaciones. 

|    Key    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.ShareNearby.IsAllowed.IntuneMAMOnly    |    **True** (valor predeterminado) habilita la característica Compartir cercanos para la cuenta profesional o educativa.<br>**False** deshabilita la característica Compartir cercanos para la cuenta profesional o educativa.    |
|    com.microsoft.office.TransferFiles.IsAllowed.IntuneMAMOnly    |    **True** (valor predeterminado) habilita la característica Transferir archivos para la cuenta profesional o educativa.<br>**False** deshabilita la característica Transferir archivos para la cuenta profesional o educativa.    |

### <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Implementación de escenarios de configuración de aplicaciones con Microsoft Endpoint Manager

Si usa Microsoft Endpoint Manager como proveedor de administración de aplicaciones móviles, vea [Agregar directivas de configuración para aplicaciones administradas sin inscripción de dispositivos](app-configuration-policies-managed-app.md) para saber cómo crear una directiva de configuración de aplicaciones administradas para escenarios de configuración de aplicaciones de protección de datos. Una vez creada la configuración, puede asignar la directiva a grupos de usuarios.

## <a name="next-steps"></a>Pasos siguientes

- [¿Qué son las directivas de protección de aplicaciones?](app-protection-policy.md) 
- [Directivas de configuración de aplicaciones para Microsoft Intune](app-configuration-policies-overview.md)