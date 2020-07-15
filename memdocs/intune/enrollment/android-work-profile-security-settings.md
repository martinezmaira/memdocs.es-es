---
title: Marco de trabajo de configuración de seguridad de Android Enterprise
titleSuffix: Microsoft Intune
description: Conozca las restricciones y los valores de configuración sugeridos para seguridad básica y alta de dispositivos Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05d0cb3db60ed0f54a66bc4128e5528e789537a8
ms.sourcegitcommit: d647eefa23c8849f49584442df568284d51d7525
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86195708"
---
# <a name="android-enterprise-work-profile-security-configurations"></a>Configuraciones de seguridad del perfil de trabajo de Android Enterprise

Como parte del [marco de configuración de la seguridad de Android Enterprise](android-configuration-framework.md), aplique la siguiente configuración a los usuarios móviles del perfil de trabajo de Android Enterprise. Para más información sobre cada configuración de directiva, consulte [Configuración de Android Enterprise para marcar los dispositivos como compatibles o no compatibles mediante Intune](../protect/compliance-policy-create-android-for-work.md#work-profile) y [Configuración de dispositivos de Android Enterprise para permitir o restringir características mediante Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Al elegir la configuración, asegúrese de revisar y clasificar los escenarios de uso. Luego, configure los usuarios siguiendo las instrucciones correspondientes al nivel de seguridad elegido. Puede ajustar la configuración sugerida en función de las necesidades de su organización. Asegúrese de que el equipo de seguridad evalúe el entorno de amenazas, los posibles riesgos y cómo afecta a la usabilidad.

En el caso de los dispositivos de perfil de trabajo de propiedad personal, se recomiendan dos marcos de configuración de la seguridad:

- [Seguridad básica del perfil de trabajo (nivel 1)](#work-profile-basic-security) 
- [Seguridad alta del perfil de trabajo (nivel 3)](#work-profile-high-security) 

> [!Note]
> Debido a la configuración disponible para los dispositivos de perfil de trabajo de Android Enterprise, no hay ninguna oferta de seguridad mejorada (nivel 2). La configuración disponible no justifica una diferencia entre el nivel 1 y el nivel 2.

## <a name="work-profile-basic-security"></a>Seguridad básica del perfil de trabajo

El nivel 1 es la configuración de seguridad mínima recomendada para los dispositivos personales en los que los usuarios tienen acceso a los datos de trabajo o educativos. Esta configuración se puede aplicar a la mayoría de los usuarios móviles. Algunos de los controles pueden afectar a la experiencia del usuario.

### <a name="device-compliance"></a>Cumplimiento de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| ATP de Microsoft Defender | Solicitar que el dispositivo tenga o esté por debajo de la puntuación de riesgo de la máquina | No configurado ||
| Estado del dispositivo | Dispositivos con acceso "root" | Bloquear ||
| Estado del dispositivo | Requerir que el dispositivo tenga el nivel de amenaza del dispositivo | No configurado||
| Estado del dispositivo | Google Play Services está configurado | Requerir ||
| Estado del dispositivo | Proveedor de seguridad actualizada | Requerir ||
| Estado del dispositivo | Atestación de dispositivo SafetyNet | Comprobar integridad básica y dispositivos certificados | Esta opción configura la certificación SafetyNet de Google en los dispositivos de los usuarios finales. La integridad básica valida la integridad del dispositivo. Por ejemplo, dispositivos con rooting, emuladores, dispositivos virtuales y cualquier otro dispositivo con signos de error de integridad básica por manipulación.<p>La opción de integridad básica y dispositivos certificados valida la compatibilidad del dispositivo con los servicios de Google. Solo superan esta comprobación aquellos dispositivos que no se han manipulado y están certificados por Google. |
| Propiedades de dispositivos | Versión de SO mínima | Formato: Principal.Secundaria<br>Ejemplo: 5.0| Microsoft recomienda configurar la versión principal mínima de Android para que coincida con las versiones de Android compatibles con las aplicaciones de Microsoft. Los OEM y los dispositivos que se adhieren a los requisitos recomendados de Android Enterprise deben ser compatibles con la versión de publicación actual y una actualización posterior. Actualmente, Android recomienda Android 8.0 y versiones posteriores para los profesionales que trabajan con datos. Consulte [Requisitos recomendados de Android Enterprise](https://www.android.com/enterprise/recommended/requirements/) para encontrar las recomendaciones más recientes de Android. |
| Propiedades de dispositivos | Versión de SO máxima | No configurado ||
| Seguridad del sistema | Requerir una contraseña para desbloquear dispositivos móviles | Requerir ||
| Seguridad del sistema | Tipo de contraseña obligatoria | Numérica compleja | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Seguridad del sistema | Longitud mínima de la contraseña | 6 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Seguridad del sistema | Máximo de minutos de inactividad antes de solicitar la contraseña| 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas.|
| Seguridad del sistema | Número de días hasta que expire la contraseña| No configurado | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Seguridad del sistema | Número de contraseñas anteriores que no se pueden reutilizar | No configurado | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Seguridad del sistema | Cifrado de almacenamiento de datos en el dispositivo | Requerir ||
| Seguridad del sistema | Bloquear aplicaciones de orígenes desconocidos | Bloquear ||
| Seguridad del sistema | Integridad en tiempo de ejecución de la aplicación Portal de empresa | Requerir ||
| Seguridad del sistema | Bloquear depuración USB en el dispositivo | Bloquear | Aunque esta configuración bloquea la depuración mediante un dispositivo USB, también deshabilita la capacidad de recopilar registros que pueden ser útiles para solucionar problemas. |
| Seguridad del sistema | Nivel mínimo de actualización de seguridad | No configurado | Los dispositivos Android pueden recibir actualizaciones de seguridad mensuales, pero la versión depende del OEM o de los operadores. Las organizaciones deben asegurarse de que los dispositivos Android implementados reciban actualizaciones de seguridad antes de implementar esta configuración. Consulte [Boletines de seguridad de Android](https://source.android.com/security/bulletin/) para información sobre las versiones de actualizaciones más recientes. |
| Acciones de no cumplimiento | Marcar el dispositivo como no conforme | Inmediatamente | De forma predeterminada, la directiva está configurada para marcar el dispositivo como no conforme. Hay otras acciones disponibles. Para más información, consulte [Configuración de acciones para dispositivos no compatibles en Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Restricciones de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| Configuración de perfil de trabajo | Copiar y pegar entre perfiles personales y de trabajo | Bloquear ||
| Configuración de perfil de trabajo | Uso compartido de datos entre el perfil profesional y el personal | Las aplicaciones de un perfil de trabajo pueden controlar la solicitud de uso compartido desde un perfil personal ||
| Configuración de perfil de trabajo | Notificaciones del perfil profesional con dispositivo bloqueado | No configurado | El bloqueo de esta configuración garantiza que los datos confidenciales no se exponen en las notificaciones del perfil de trabajo, lo que puede afectar a la usabilidad. |
| Configuración de perfil de trabajo | Permisos de aplicación predeterminados | Valor predeterminado del dispositivo | Los administradores deben revisar y ajustar los permisos concedidos por las aplicaciones que implementan. |
| Configuración de perfil de trabajo | Agregar y quitar cuentas | Bloquear ||
| Configuración de perfil de trabajo | Uso compartido de contactos a través de Bluetooth | Habilitar | De forma predeterminada, el acceso a los contactos de trabajo no está disponible en otros dispositivos, como en los automóviles mediante la integración con Bluetooth. Al habilitar esta opción, se mejora la experiencia de usuario sin manos. Sin embargo, el dispositivo Bluetooth puede almacenar en caché los contactos tras la primera conexión. Al implementar esta configuración, las organizaciones deben pensar en el equilibrio entre los escenarios de usabilidad y los problemas de protección de datos. |
| Configuración de perfil de trabajo | Captura de pantalla | Bloquear ||
| Configuración de perfil de trabajo | Mostrar el identificador de llamada de contacto profesional en el perfil personal | No configurado ||
| Configuración de perfil de trabajo | Buscar contactos profesionales del perfil personal | No configurado | Impedir que los usuarios accedan a los contactos de trabajo desde el perfil personal pueden afectar a determinados escenarios de usabilidad, como la mensajería de texto y las experiencias de marcado en el perfil personal. Al implementar esta configuración, las organizaciones deben pensar en el equilibrio entre los escenarios de usabilidad y los problemas de protección de datos. |
| Configuración de perfil de trabajo | Cámara | No configurado ||
| Configuración de perfil de trabajo | Permitir widgets de las aplicaciones del perfil de trabajo | Habilitar ||
| Configuración de perfil de trabajo | Requerir contraseña del perfil de trabajo | Requerir ||
| Configuración de perfil de trabajo | Longitud mínima de la contraseña | 6 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Configuración de perfil de trabajo | Cantidad máxima de minutos de inactividad hasta que el perfil de trabajo se bloquea| 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Configuración de perfil de trabajo | Número de errores de inicio de sesión antes de eliminar los datos del perfil de trabajo| 10 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Configuración de perfil de trabajo | Expiración de contraseña (días) | No configurado | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Configuración de perfil de trabajo | Tipo de contraseña obligatoria | Numérica compleja ||
| Configuración de perfil de trabajo | Impedir la reutilización de contraseñas anteriores | No configurado | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas.|
| Configuración de perfil de trabajo | Desbloqueo con huella digital | No configurado ||
| Configuración de perfil de trabajo | Smart Lock y otros agentes de confianza | No configurado |||
| Contraseña del dispositivo | Longitud mínima de la contraseña | 6 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Contraseña del dispositivo | Máximo de minutos de inactividad hasta que se bloquea la pantalla | 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Contraseña del dispositivo | Número de errores de inicio de sesión antes de borrar el dispositivo | 10 | Esta configuración desencadena un borrado del perfil de trabajo y no un borrado del dispositivo. |
| Contraseña del dispositivo | Expiración de contraseña (días) | No configurado | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Contraseña del dispositivo | Tipo de contraseña obligatoria | Numérica compleja ||
| Contraseña del dispositivo | Impedir la reutilización de contraseñas anteriores | No configurado | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Contraseña del dispositivo | Desbloqueo con huella digital | No configurado ||
| Contraseña del dispositivo | Smart Lock y otros agentes de confianza | No configurado ||
| Seguridad del sistema | Examen de amenazas en las aplicaciones | Requerir | Este valor garantiza que el examen de verificación de aplicaciones de Google está activado para los dispositivos de los usuarios finales. Si se ha configurado, se bloqueará el acceso al usuario hasta que se active el examen de aplicaciones de Google en su dispositivo Android. |
| Seguridad del sistema | Impedir la instalación de aplicaciones de orígenes desconocidos en el perfil personal | Bloquear ||

> [!Note]
> Cuando se habilita el perfil de trabajo de Android Enterprise, se configura "Un bloqueo" de forma predeterminada para combinar los códigos de acceso del perfil de trabajo y del dispositivo. Esta opción se puede deshabilitar para separar los códigos de acceso del perfil de trabajo y del dispositivo, si es necesario, en la configuración del perfil de trabajo.

## <a name="work-profile-high-security"></a>Alta seguridad del perfil de trabajo

El nivel 3 es la configuración recomendada para los dispositivos que usan los usuarios o grupos que son exclusivamente de alto riesgo. Por ejemplo, usuarios que controlan datos muy delicados cuya divulgación no autorizada causaría pérdidas materiales considerables. Una organización que pueda ser el objetivo de adversarios sofisticados y con una buena financiación deberían aplicar las restricciones adicionales que se indican a continuación. Esta configuración amplía la configuración del nivel 1:
- implementación de Mobile Threat Defense o ATP de Microsoft defender.
- restricción de escenarios de datos de perfil de trabajo.
- prescribir directivas de contraseña más seguras.

La configuración de directiva que se aplica en el nivel 3 incluye todas las configuraciones de directiva recomendadas para el nivel 1. Sin embargo, los valores que se muestran a continuación incluyen solo los que se han agregado o cambiado. Esta configuración puede tener un impacto ligeramente mayor en los usuarios o las aplicaciones. Aplica un nivel de seguridad más adecuado para los riesgos a los que se enfrentan los usuarios con acceso a información confidencial en los dispositivos móviles.

### <a name="device-compliance"></a>Cumplimiento de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| ATP de Microsoft Defender | Solicitar que el dispositivo tenga o esté por debajo de la puntuación de riesgo de la máquina | Borrar | Esta configuración requiere ATP de Microsoft Defender. Para más información, consulte la aplicación del cumplimiento de [ATP de Microsoft Defender con acceso condicional en Intune](../protect/advanced-threat-protection.md).<p>Los clientes deben considerar la posibilidad de implementar ATP de Microsoft Defender o una solución de defensa contra frente a amenazas para dispositivos móviles. No es necesario implementar ambas. |
| Estado del dispositivo | Requerir que el dispositivo tenga el nivel de amenaza del dispositivo | Protegido | Esta configuración requiere un producto de defensa frente a amenazas para dispositivos móviles. Para más información, consulte [Mobile Threat Defense para dispositivos inscritos](../protect/mtd-device-compliance-policy-create.md).<p>Los clientes deben considerar la posibilidad de implementar ATP de Microsoft Defender o una solución de defensa contra frente a amenazas para dispositivos móviles. No es necesario implementar ambas.|
| Propiedades de dispositivos | Versión de SO mínima | Formato: Principal.Secundaria<br>Ejemplo: 8.0| Microsoft recomienda configurar la versión principal mínima de Android para que coincida con las versiones de Android compatibles con las aplicaciones de Microsoft. Los OEM y los dispositivos que se adhieren a los requisitos recomendados de Android Enterprise deben ser compatibles con la versión de publicación actual y una actualización posterior. Actualmente, Android recomienda Android 8.0 y versiones posteriores para los profesionales que trabajan con datos. Consulte Requisitos de Android Enterprise Recommended para conocer las recomendaciones más recientes de Android. |
| Seguridad del sistema | Número de días hasta que expire la contraseña | 365 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Seguridad del sistema | Número de contraseñas anteriores que no se pueden reutilizar | 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |


### <a name="device-restrictions"></a>Restricciones de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| Configuración de perfil de trabajo | Notificaciones del perfil profesional con dispositivo bloqueado | Bloquear | El bloqueo de esta configuración garantiza que los datos confidenciales no se exponen en las notificaciones del perfil de trabajo, lo que puede afectar a la usabilidad. |
| Configuración de perfil de trabajo | Uso compartido de contactos a través de Bluetooth | No configurado | De forma predeterminada, el acceso a los contactos de trabajo no está disponible en otros dispositivos, como en los automóviles mediante la integración con Bluetooth. Al habilitar esta opción, se mejora la experiencia de usuario sin manos. Sin embargo, el dispositivo Bluetooth puede almacenar en caché los contactos tras la primera conexión. Al implementar esta configuración, las organizaciones deben pensar en el equilibrio entre los escenarios de usabilidad y los problemas de protección de datos. |
| Configuración de perfil de trabajo | Buscar contactos profesionales del perfil personal | Bloquear | Impedir que los usuarios accedan a los contactos de trabajo desde el perfil personal pueden afectar a determinados escenarios de usabilidad, como la mensajería de texto y las experiencias de marcado en el perfil personal. Al implementar esta configuración, las organizaciones deben pensar en el equilibrio entre los escenarios de usabilidad y los problemas de protección de datos. |
| Configuración de perfil de trabajo | Permitir widgets de las aplicaciones del perfil de trabajo | No configurado ||
| Configuración de perfil de trabajo | Número de errores de inicio de sesión antes de eliminar los datos del perfil de trabajo | 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Configuración de perfil de trabajo | Expiración de contraseña (días) | 365 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Configuración de perfil de trabajo | Impedir la reutilización de contraseñas anteriores | 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Configuración de perfil de trabajo | Smart Lock y otros agentes de confianza | Bloquear ||
| Contraseña del dispositivo | Número de errores de inicio de sesión antes de borrar el dispositivo | 5 | Esta configuración desencadena un borrado del perfil de trabajo y no un borrado del dispositivo. |
| Contraseña del dispositivo | Expiración de contraseña (días) | 365 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Contraseña del dispositivo | Impedir la reutilización de contraseñas anteriores | 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |

## <a name="next-steps"></a>Pasos siguientes

Los administradores pueden incorporar los niveles de configuración anteriores dentro de su metodología de implementación en anillo para su uso en producción y pruebas mediante la importación de las [plantillas JSON del marco de configuración de seguridad de Android Enterprise](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) de ejemplo con [scripts de PowerShell de Intune](https://github.com/microsoftgraph/powershell-intune-samples).
