---
title: Marco de protección de datos mediante directivas de protección de aplicaciones
titleSuffix: Microsoft Intune
description: Descubra cómo las directivas de protección de aplicaciones (APP) garantizan que los datos de la organización siguen siendo seguros o se encuentran en una aplicación administrada, esté inscrito o no el dispositivo.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: cfb0012dfc2cedb72c64a54c16b567dffff84c9e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342301"
---
# <a name="data-protection-framework-using-app-protection-policies"></a>Marco de protección de datos mediante directivas de protección de aplicaciones 

A medida que más organizaciones implementan las estrategias de dispositivos móviles para acceder a los datos profesionales o educativos, la protección contra la pérdida de datos se vuelve primordial. La solución de administración de aplicaciones móviles de Intune para protegerse frente a la pérdida de datos consiste en las directivas de protección de aplicaciones (APP). Las APP son reglas que garantizan que los datos de la organización siguen siendo seguros o se encuentran en una aplicación administrada, esté inscrito o no el dispositivo. Para obtener más información, consulte [Introducción a las directivas de protección de aplicaciones](app-protection-policy.md).

Al configurar las directivas de protección de aplicaciones, las distintas configuraciones y opciones permiten a las organizaciones adaptar la protección a sus necesidades específicas. Debido a esta flexibilidad, puede que no sea obvio qué permutación de la configuración de directivas es necesaria para implementar un escenario completo. Para ayudar a las organizaciones a priorizar los esfuerzos de protección de puntos de conexión de cliente, Microsoft ha introducido una nueva taxonomía para las [configuraciones de seguridad en Windows 10](https://aka.ms/secconframework). Asimismo, Intune aprovecha una taxonomía similar para su marco de protección de datos de APP para la administración de aplicaciones móviles.  

El marco de configuración de protección de datos de APP se organiza en tres escenarios de configuración distintos:

- Protección de datos empresariales básica de nivel 1: Microsoft la recomienda como configuración de protección de datos mínima para un dispositivo de empresa.

- Protección de datos empresariales mejorada de nivel 2: Microsoft recomienda esta configuración para los dispositivos con los que los usuarios acceden a información confidencial. Esta configuración es aplicable a la mayoría de los usuarios móviles que acceden a datos profesionales o educativos. Algunos de los controles pueden afectar a la experiencia del usuario.

- Protección de datos empresariales alta de nivel 3: Microsoft recomienda esta configuración para los dispositivos que ejecuta una organización con un equipo de seguridad más grande o más sofisticado, o para usuarios o grupos específicos que tienen un riesgo único (por ejemplo, una organización que haya identificado usuarios que controlan datos cuyo robo afectaría directa y gravemente al precio de sus acciones). Una organización que pueda ser el objetivo de adversarios sofisticados y con una gran financiación debería elegir esta configuración.

## <a name="app-data-protection-framework-deployment-methodology"></a>Metodología de implementación del marco de protección de datos de APP

Como con cualquier implementación de software, característica o configuración nueva, Microsoft recomienda invertir en una metodología de anillo para probar la validación antes de implementar el marco de protección de datos de APP. La definición de anillos de implementación suele ser un evento único (o al menos poco frecuente), pero el equipo de TI debe revisar estos grupos para asegurarse de que la secuenciación sigue siendo correcta.

Microsoft recomienda el siguiente enfoque de anillo de implementación para el marco de protección de datos de APP:

| Anillo de implementación  | Inquilino  | Equipos de evaluación  | Salida  | Escala de tiempo  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Control de calidad  | Inquilino de preproducción  | Propietarios de funcionalidades móviles, seguridad, evaluación de riesgos, privacidad, experiencia de usuario  | Validación del escenario funcional, documentación de borrador  | De 0 a 30 días  |
| Vista previa  | Inquilino de producción  | Propietarios de funcionalidades móviles, experiencia de usuario  | Validación del escenario de usuario final, documentación orientada al usuario  | De 7 a 14 días, después del control de calidad  |
| Producción  | Inquilino de producción  | Propietarios de funcionalidades móviles, departamento de soporte técnico de TI  | No aplicable  | De 7 días a varias semanas, después de la versión preliminar  |

Como se indica en la tabla anterior, todos los cambios en las directivas de protección de aplicaciones deben realizarse en primer lugar en un entorno de preproducción para comprender las implicaciones de la configuración de la directiva. Una vez completadas las pruebas, los cambios pueden pasarse a producción y aplicarse a un subconjunto de usuarios de producción, que generalmente suelen ser el departamento de TI y otros grupos aplicables. Por último, la implementación puede completarse en el resto de la comunidad de usuarios móviles. La implementación en producción puede tardar más tiempo en función de la escala de impacto en relación con el cambio. Si no afecta al usuario, el cambio se debe implementarse rápidamente; por el contrario, si sí que le afecta, es posible que la implementación tenga que realizarse más despacio debido a la necesidad de comunicar los cambios a los usuarios.

Al probar los cambios en APP, tenga en cuenta el [tiempo de entrega](app-protection-policy-delivery.md). El estado de entrega de APP para un usuario determinado puede supervisarse. Para más información, consulte [Supervisión de las directivas de protección de aplicaciones](app-protection-policies-monitor.md).

La configuración de APP individual para cada aplicación se puede validar en dispositivos que usen Edge y la dirección URL *about:Intunehelp*. Para obtener más información, consulte [Revisión de los registros de protección de las aplicaciones cliente](app-protection-policy-settings-log.md) y [Administración del acceso web mediante Microsoft Edge con Microsoft Intune](manage-microsoft-edge.md#use-microsoft-edge-on-ios-to-access-managed-app-logs).

## <a name="app-data-protection-framework-settings"></a>Configuración del marco de protección de datos mediante APP

La siguiente configuración de directiva de protección de aplicaciones debe estar habilitada para las aplicaciones correspondientes y asignada a todos los usuarios móviles. Para obtener más información sobre cada configuración de directiva, consulte [Configuración de directivas de protección de aplicaciones de iOS](app-protection-policy-settings-ios.md) y [Configuración de directivas de protección de aplicaciones de Android](app-protection-policy-settings-android.md).

Microsoft recomienda revisar y clasificar los escenarios de uso y, después, configurar los usuarios mediante las instrucciones prescriptivas para ese nivel. Como con cualquier marco de trabajo, es posible que sea necesario ajustar la configuración dentro de un nivel correspondiente en función de las necesidades de la organización, ya que la protección de datos debe evaluar el entorno de amenazas, el apetito del riesgo y el impacto en la facilidad de uso.  

### <a name="apps-to-include-in-the-app-protection-policies"></a>Aplicaciones que se van a incluir en las directivas de protección de aplicaciones  

Para cada directiva de protección de aplicaciones, se deben incluir las siguientes aplicaciones principales de Microsoft:

- Edge
- Excel
- Office
- OneDrive
- OneNote
- Outlook
- PowerPoint
- Microsoft Teams
- Microsoft To-Do
- Word
- Microsoft SharePoint

Las directivas deben incluir otras aplicaciones de Microsoft basadas en necesidades empresariales, aplicaciones públicas de terceros adicionales que han integrado el SDK de Intune que se usa en la organización, así como aplicaciones de línea de negocio que han integrado el [SDK de Intune](../developer/app-sdk.md) (o se han ajustado).

### <a name="level-1-enterprise-basic-data-protection"></a>Protección de datos empresariales básica de nivel 1

El nivel 1 es la configuración mínima de protección de datos para un dispositivo móvil empresarial. Esta configuración reemplaza la necesidad de directivas básicas de acceso a dispositivos de Exchange Online, ya que requiere un PIN para acceder a los datos profesionales o educativos, cifra los datos de la cuenta profesional o educativa y proporciona la capacidad de borrar de forma selectiva los datos escolares o de trabajo. Pero, a diferencia de las directivas de acceso a dispositivos de Exchange Online, las siguientes opciones de directiva de protección de aplicaciones se aplican a todas las aplicaciones seleccionadas en la directiva, lo que garantiza que el acceso a los datos está protegido más allá de los escenarios de mensajería móvil.

Las directivas de nivel 1 exigen un nivel de acceso a datos razonable a la vez que minimizan el impacto para los usuarios y reflejan los valores predeterminados de protección de datos y de los requisitos de acceso al crear una directiva de protección de aplicaciones en Microsoft Endpoint Manager.  

#### <a name="data-protection"></a>Protección de datos

| Setting | Descripción del valor |             Valor  |             Plataforma        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| Transferencia de datos |             Realizar una copia de seguridad de datos de la organización en…  |             Allow  |             iOS/iPadOS, Android        |
| Transferencia de datos |       Enviar datos de la organización a otras aplicaciones  |             Todas las aplicaciones  |             iOS/iPadOS, Android        |
| Transferencia de datos |       Recibir datos de otras aplicaciones  |             Todas las aplicaciones  |             iOS/iPadOS, Android        |
| Transferencia de datos |       Restringir cortar, copiar y pegar entre aplicaciones  |             Cualquier aplicación  |             iOS/iPadOS, Android        |
| Transferencia de datos |       Teclados de terceros  |             Allow  |             iOS/iPadOS        |
| Transferencia de datos |       Teclados aprobados  |             No se requiere  |             Android        |
| Transferencia de datos |       Captura de pantalla y Asistente de Google  |             Allow  |             Android        |
| Cifrado |             Cifrar datos de la organización  |             Requerir  |             iOS/iPadOS, Android        |
| Cifrado |       Cifrar datos de la organización en los dispositivos inscritos  |             Requerir  |             Android        |
| Funcionalidad  |             Sincronizar la aplicación con la aplicación de contactos nativa  |             Allow  |             iOS/iPadOS, Android        |
| Funcionalidad  |       Impresión de datos de la organización  |             Allow  |             iOS/iPadOS, Android        |
| Funcionalidad  |       Restringir la transferencia de contenido web con otras aplicaciones  |             Cualquier aplicación  |             iOS/iPadOS, Android        |
| Funcionalidad  |       Notificaciones de datos de la organización  |             Allow  |             iOS/iPadOS, Android        |

#### <a name="access-requirements"></a>Requisitos de acceso 

| Setting  | Valor  | Plataforma  | Notas  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PIN para acceder  | Requerir  | iOS/iPadOS, Android  |   |
| Tipo de PIN  | Numérico  | iOS/iPadOS, Android  |   |
| PIN simple  | Allow  | iOS/iPadOS, Android  |   |
| Seleccionar la longitud mínima del PIN  | 4  | iOS/iPadOS, Android  |   |
| Biometría en lugar de PIN para el acceso  | Allow  | iOS/iPadOS, Android  |   |
| Invalidar biometría en lugar de PIN para el acceso  | Requerir  | iOS/iPadOS, Android  |   |
| Tiempo de espera (minutos de actividad)  | 720  | iOS/iPadOS, Android  |   |
| Face ID en lugar de PIN para el acceso  | Allow  | iOS/iPadOS  |   |
| Restablecimiento del PIN después de un número de días  | No  | iOS/iPadOS, Android  |   |
| PIN de aplicación cuando está establecido el PIN del dispositivo  | Requerir  | iOS/iPadOS, Android  | Si el dispositivo está inscrito en Intune, los administradores pueden establecer este valor en "No es necesario" si están aplicando un PIN de dispositivo seguro mediante una directiva de cumplimiento de dispositivos.  |
| Credenciales de cuenta profesional o educativa para el acceso  | No se requiere  | iOS/iPadOS, Android  |   |
| Volver a comprobar los requisitos de acceso tras (minutos de inactividad)  | 30  | iOS/iPadOS, Android  |   |

#### <a name="conditional-launch"></a>Inicio condicional 

| Setting | Descripción del valor |          Valor/acción  |          Plataforma        | Notas |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Condiciones de la aplicación |       N.º máximo de intentos de PIN  |          5 / Restablecer PIN  |          iOS/iPadOS, Android  |                  |
| Condiciones de la aplicación |       Período de gracia sin conexión  |          720 / Bloquear acceso (minutos)  |          iOS/iPadOS, Android  |                  |
| Condiciones de la aplicación |       Período de gracia sin conexión  |          90 / Borrar datos (días)  |          iOS/iPadOS, Android  |                  |
| Condiciones de dispositivo  |       Dispositivos con jailbreak o rooting  |        N/D / Bloquear acceso  |          iOS/iPadOS, Android  |                  |
| Condiciones de dispositivo  |       Certificación de dispositivo SafetyNet  |          Integridad básica y dispositivos certificados / Bloquear acceso  |          Android  |          <p>Este valor configura la atestación de SafetyNet de Google en dispositivos de usuarios finales. La integridad básica valida la integridad del dispositivo. Por ejemplo, los dispositivos con rooting, los emuladores, los dispositivos virtuales y cualquier otro dispositivo con signos de manipulación no superan la integridad básica. </p><p> Integridad básica y dispositivos certificados valida la compatibilidad del dispositivo con los servicios de Google. Solo superan esta comprobación aquellos dispositivos que no se han manipulado y están certificados por Google.</p>  |
| Condiciones de dispositivo  |       Requerir examen de amenazas en las aplicaciones  |        N/D / Bloquear acceso  |          Android  |          Este valor garantiza que el examen de verificación de aplicaciones de Google está activado para los dispositivos de usuarios finales. Si se ha configurado, se bloqueará el acceso al usuario hasta que se active el examen de aplicaciones de Google en su dispositivo Android.        |

#### <a name="level-2-enterprise-enhanced-data-protection"></a>Protección de datos empresariales mejorada de nivel 2

El nivel 2 es la configuración de protección de datos recomendada como estándar para los dispositivos en los que los usuarios acceden a información más confidencial. Estos dispositivos son un objetivo natural en las empresas de hoy en día. Estas recomendaciones no suponen una gran cantidad de personal de profesionales de seguridad muy experimentados y, por tanto, deben ser accesibles para la mayoría de las organizaciones empresariales. Esta configuración amplía la de nivel 1 mediante la restricción de los escenarios de transferencia de datos y la exigencia de una versión mínima del sistema operativo.

La configuración de directiva que se aplica en el nivel 2 incluye todas las configuraciones de directiva recomendadas para el nivel 1 y solo actualiza o suma a la siguiente configuración de directiva para implementar más controles y una configuración más sofisticada que el nivel 1. Aunque esta configuración puede tener un impacto ligeramente mayor para los usuarios o las aplicaciones, aplica un nivel de protección de datos más acorde con los riesgos a los que se enfrentan los usuarios con acceso a información confidencial en dispositivos móviles.

#### <a name="data-protection"></a>Protección de datos

| Setting | Descripción del valor |             Valor  |             Plataforma        | Notas |
|---------------|----------------------------------------------------------|-----------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Transferencia de datos |       Realizar una copia de seguridad de datos de la organización en…  |          Bloquear  |          iOS/iPadOS, Android  |                  |
| Transferencia de datos |       Enviar datos de la organización a otras aplicaciones  |          Aplicaciones administradas por directivas  |          iOS/iPadOS, Android  |          <p>Con iOS/iPadOS, los administradores pueden configurar este valor para que sea "Aplicaciones administradas por directivas", "Aplicaciones administradas por directivas con uso compartido de SO" o "Aplicaciones administradas por directivas con filtrado de apertura/uso compartido". </p><p>Las aplicaciones administradas por directivas con uso compartido de SO están disponibles cuando el dispositivo también se inscribe con Intune. Esta configuración permite la transferencia de datos a otras aplicaciones administradas por directivas, así como las transferencias de archivos a otras aplicaciones administradas por Intune. </p><p>Las aplicaciones administradas por directivas con filtrado de Abrir en/Compartir del sistema operativo filtra los cuadros de diálogo correspondientes a estos filtros para mostrar solo dichas aplicaciones. </p><p> Para obtener más información, vea [Configuración de directiva de protección de aplicaciones de iOS](app-protection-policy-settings-ios.md).</p> |
| Transferencia de datos |       Guardar copias de los datos de la organización  |          Bloquear  |          iOS/iPadOS, Android  |                  |
| Transferencia de datos |       Permitir al usuario guardar copias en los servicios seleccionados  |          OneDrive para la Empresa, SharePoint Online |          iOS/iPadOS, Android  |                  |
| Transferencia de datos |       Restringir cortar, copiar y pegar entre aplicaciones  |          Aplicaciones administradas por directivas con pegar  |          iOS/iPadOS, Android  |                  |
| Transferencia de datos |       Captura de pantalla y Asistente de Google  |          Bloquear  |          Android  |                  |
| Funcionalidad |       Restringir la transferencia de contenido web con otras aplicaciones  |          Microsoft Edge  |          iOS/iPadOS, Android  |                  |
| Funcionalidad |       Notificaciones de datos de la organización  |          Bloquear datos de la organización  |          iOS/iPadOS, Android  |          Para obtener una lista de aplicaciones compatibles con esta configuración, vea [Configuración de directivas de protección de aplicaciones de iOS](app-protection-policy-settings-ios.md) y [Configuración de directivas de protección de aplicaciones de Android](app-protection-policy-settings-android.md).       |

#### <a name="conditional-launch"></a>Inicio condicional

| Setting | Descripción del valor |          Valor/acción  |          Plataforma        | Notas |
|--------------------|----------------------------|-----------------------------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Condiciones de dispositivo  |       Versión mínima del sistema operativo  |          *Formato: Major.Minor.Build <br>Ejemplo:   12.4.4* / Bloquear acceso |          iOS/iPadOS        | Microsoft recomienda configurar la versión principal mínima de iOS para que coincida con las versiones de iOS compatibles con las aplicaciones de Microsoft.   Las aplicaciones de Microsoft admiten un enfoque N-1 donde N es la versión principal actual de iOS. En el caso de los valores de versión secundaria y de compilación, Microsoft recomienda garantizar que los dispositivos estén actualizados con las actualizaciones de seguridad respectivas. Vea [Actualizaciones de seguridad de Apple](https://support.apple.com/en-us/HT201222) para obtener las recomendaciones más recientes de Apple |
| Condiciones de dispositivo  |       Versión mínima del sistema operativo  |          *Formato: Major.Minor<br>   Ejemplo: 8.0* / Bloquear acceso   |          Android        | Microsoft recomienda configurar la versión principal mínima de Android para que coincida con las versiones de Android compatibles con las aplicaciones de Microsoft. Los OEM y los dispositivos que se adhieren a los requisitos recomendados de Android Enterprise deben ser compatibles con la versión de publicación actual y una actualización posterior.   Actualmente, Android recomienda Android 8.0 y versiones posteriores para los profesionales que trabajan con datos.   Vea [Requisitos recomendados de Android Enterprise](https://www.android.com/enterprise/recommended/requirements/) para obtener las recomendaciones más recientes de Android |
| Condiciones de dispositivo  |       Versión mínima de la revisión  |          *Formato:   AAAA-MM-DD <br> Ejemplo: 2020-01-01* / Bloquear acceso  |          Android        | Los dispositivos Android pueden recibir revisiones de seguridad mensuales, pero la versión depende del OEM o los operadores. Las organizaciones deben asegurarse de que los dispositivos Android implementados reciban actualizaciones de seguridad antes de implementar esta configuración. Vea [Android Security Bulletins](https://source.android.com/security/bulletin/) (Boletines de seguridad de Android) para obtener información sobre las versiones de revisión más recientes.  |

#### <a name="level-3-enterprise-high-data-protection"></a>Protección de datos empresariales alta de nivel 3 

El nivel 3 es la configuración de protección de datos recomendada como estándar para las organizaciones con organizaciones de seguridad grandes y sofisticadas, o para usuarios y grupos que serán objetivos específicos de sus adversarios. Por lo general, estas organizaciones son el objetivo de adversarios sofisticados y con buena financiación, por lo que necesitan las restricciones y los controles adicionales descritos. Esta configuración amplías las opciones de nivel 2 mediante la restricción de escenarios de transferencia de datos adicionales, el aumento de la complejidad de la configuración del PIN y la adición de detección de amenazas móviles.  

La configuración de directiva que se aplica en el nivel 3 incluye todas las configuraciones de directiva recomendadas para los niveles 2 y 1 y solo actualiza o suma a la siguiente configuración de directiva para implementar configuración de protección de datos y controles estrictos. Esta configuración de directiva puede tener un impacto potencialmente significativo en los usuarios o en las aplicaciones, con lo que se impone un nivel de seguridad acorde con los riesgos a los que se enfrentan las organizaciones de destino.  

#### <a name="data-protection"></a>Protección de datos

| Setting | Descripción del valor |             Valor  |             Plataforma        | Notas |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| Transferencia de datos |       Recibir datos de otras aplicaciones  |          Aplicaciones administradas por directivas  |          iOS/iPadOS, Android         |  |
| Transferencia de datos |       Teclados de terceros  |          Bloquear  |          iOS/iPadOS        | En iOS, esto impide que todos los teclados de terceros funcionen dentro de la aplicación.  |
| Transferencia de datos |       Teclados aprobados  |          Requerir  |          Android        | Con Android, se deben seleccionar los teclados para poder usarlos en función de los dispositivos Android implementados.  |
| Transferencia de datos |       Seleccionar teclados para su aprobación  |          *Agregar o quitar teclados*  |          Android        | Con Android, se deben seleccionar los teclados para poder usarlos en función de los dispositivos Android implementados.  |
| Funcionalidad |       Impresión de datos de la organización  |          Bloquear  |          iOS/iPadOS, Android         |  |

#### <a name="access-requirements"></a>Requisitos de acceso

|       Setting  |          Valor  |          Plataforma  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       PIN simple  |          Bloquear  |          iOS/iPadOS, Android  |
|       Seleccionar la longitud mínima del PIN  |          6  |          iOS/iPadOS, Android  |
|       Restablecimiento del PIN después de un número de días  |          Sí  |          iOS/iPadOS, Android  |
|       Número de días  |          365  |          iOS/iPadOS, Android  |

#### <a name="conditional-launch"></a>Inicio condicional

| Setting | Descripción del valor |          Valor/acción  |          Plataforma        | Notas |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       Condiciones de dispositivo  |          Dispositivos con jailbreak o liberados  |        N/D / Borrar datos  |          iOS/iPadOS, Android        |  |
|       Condiciones de dispositivo  |          Nivel de amenaza máximo permitido  |          Protegido / Bloquear acceso  |          iOS/iPadOS, Android        | <p>Los dispositivos no inscritos pueden inspeccionarse en busca de amenazas con Mobile Threat Defense. Para obtener más información, vea [Mobile Threat Defense para  dispositivos no inscritos](https://aka.ms/mtdmamdocs).      </p><p>     Si el dispositivo está inscrito, este valor puede omitirse en favor de la implementación de Mobile Threat Defense para dispositivos inscritos. Para obtener más información, vea [Mobile Threat Defense para  dispositivos no inscritos](../protect/mtd-device-compliance-policy-create.md).</p> |

## <a name="next-steps"></a>Pasos siguientes

Los administradores pueden incorporar los niveles de configuración anteriores dentro de su metodología de implementación en anillo para su uso en producción y pruebas mediante la importación de [plantillas JSON del marco de configuración de directiva de Intune App Protection](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) con [scripts de PowerShell de Intune](https://github.com/microsoftgraph/powershell-intune-samples).

## <a name="see-also"></a>Vea también

- [Creación e implementación de directivas de protección de aplicaciones con Microsoft Intune](app-protection-policies.md)
- [Configuración de directivas de protección de aplicaciones Android disponibles con Microsoft Intune](app-protection-policy-settings-android.md)
- [Configuración de directivas de protección de aplicaciones iOS/iPadOS disponibles con Microsoft Intune](app-protection-policy-settings-ios.md)
- Las aplicaciones de terceros, como la aplicación móvil de Salesforce, funcionan con Intune de formas específicas para proteger los datos corporativos. Para más información sobre cómo la aplicación de Salesforce funciona con Intune en particular (incluida la configuración de la aplicación de MDM), vea [Salesforce App and Microsoft Intune](https://gallery.technet.microsoft.com/Salesforce-App-and-Intune-c47d44ee/file/188000/1/Salesforce%20App%20and%20Intune%20for%20external.pdf) (Aplicación de Salesforce y Microsoft Intune).
