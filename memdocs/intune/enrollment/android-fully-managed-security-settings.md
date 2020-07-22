---
title: Configuraciones de seguridad totalmente administrada de Android Enterprise
titleSuffix: Microsoft Intune
description: Conozca la configuración sugerida para la seguridad básica, mejorada y alta totalmente administrada de Android Enterprise.
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
ms.openlocfilehash: 01c8c0ffba349966c99e1cbd90dbdfc10a5c9782
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461171"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Configuraciones de seguridad totalmente administrada de Android Enterprise

Como parte del [marco de configuración de seguridad de Android Enterprise](android-configuration-framework.md), aplique la siguiente configuración para los usuarios móviles totalmente administrados de Android Enterprise. Para más información sobre cada configuración de directiva, consulte [Configuración del propietario del dispositivo de Android Enterprise para marcar los dispositivos como compatibles o no compatibles mediante Intune](../protect/compliance-policy-create-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile) y [Configuración de dispositivos de Android Enterprise para permitir o restringir características mediante Intune](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile).

Al elegir la configuración, asegúrese de revisar y clasificar los escenarios de uso. Luego, configure los usuarios siguiendo las instrucciones correspondientes al nivel de seguridad elegido. Puede ajustar la configuración sugerida en función de las necesidades de su organización. Asegúrese de que el equipo de seguridad evalúe el entorno de amenazas, los posibles riesgos y cómo afecta a la usabilidad.

En el caso de los dispositivos corporativos totalmente administrados, hay tres marcos de configuración de seguridad recomendados:

- [Seguridad básica totalmente administrada (nivel 1)](#fully-managed-basic-security) 
- [Seguridad mejorada totalmente administrada (nivel 2)](#fully-managed-enhanced-security)
- [Alta seguridad totalmente administrada (nivel 3)](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>Seguridad básica totalmente administrada

El nivel 1 es la configuración de seguridad mínima recomendada para los dispositivos móviles que pertenecen a la organización.

Las directivas de nivel 1 exigen un nivel de acceso a los datos razonable a la vez que minimizan los efectos para los usuarios. Para ello se aplican directivas de contraseñas, una versión mínima del sistema operativo, la certificación de dispositivo SafetyNet y la deshabilitación de determinadas funciones del dispositivo (como las transferencias de archivos USB). 

### <a name="device-compliance"></a>Cumplimiento de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| ATP de Microsoft Defender | Solicitar que el dispositivo tenga o esté por debajo de la puntuación de riesgo de la máquina | No configurado ||
| Estado del dispositivo | Requerir que el dispositivo tenga el nivel de amenaza del dispositivo | No configurado||
| Estado del dispositivo | Atestación de dispositivo SafetyNet | Comprobar integridad básica y dispositivos certificados | Esta opción configura la certificación SafetyNet de Google en los dispositivos de los usuarios finales. La integridad básica valida la integridad del dispositivo. Por ejemplo, dispositivos con rooting, emuladores, dispositivos virtuales y cualquier otro dispositivo con signos de error de integridad básica por manipulación.<br>La opción de integridad básica y dispositivos certificados valida la compatibilidad del dispositivo con los servicios de Google. Solo superan esta comprobación aquellos dispositivos que no se han manipulado y están certificados por Google. |
| Propiedades de dispositivos | Versión de SO mínima | Formato: Principal.Secundaria<br>Ejemplo: 8.0| Microsoft recomienda configurar la versión principal mínima de Android para que coincida con las versiones de Android compatibles con las aplicaciones de Microsoft. Los OEM y los dispositivos que se adhieren a los requisitos recomendados de Android Enterprise deben ser compatibles con la versión de publicación actual y una actualización posterior. Actualmente, Android recomienda Android 8.0 y versiones posteriores para los profesionales que trabajan con datos. Consulte [Requisitos recomendados de Android Enterprise](https://www.android.com/enterprise/recommended/requirements/) para encontrar las recomendaciones más recientes de Android. |
| Propiedades de dispositivos | Versión de SO máxima | No configurado ||
| Propiedades de dispositivos | Nivel mínimo de actualización de seguridad | No configurado | Los dispositivos Android pueden recibir actualizaciones de seguridad mensuales, pero la versión depende del OEM o de los operadores. Las organizaciones deben asegurarse de que los dispositivos Android implementados reciban actualizaciones de seguridad antes de implementar esta configuración. Consulte [Boletines de seguridad de Android](https://source.android.com/security/bulletin/) para información sobre las versiones de actualizaciones más recientes. |
| Seguridad del sistema | Requerir una contraseña para desbloquear dispositivos móviles | Requerir ||
| Seguridad del sistema | Tipo de contraseña obligatoria | Numérica compleja | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Seguridad del sistema | Longitud mínima de la contraseña | 6 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Seguridad del sistema | Máximo de minutos de inactividad antes de solicitar la contraseña| 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas.|
| Seguridad del sistema | Número de días hasta que expire la contraseña| No configurado ||
| Seguridad del sistema |    Número de contraseñas requeridas antes de que el usuario pueda reusar una | No configurado ||
| Seguridad del sistema | Cifrado de almacenamiento de datos en el dispositivo | Requerir ||
| Acciones de no cumplimiento | Marcar el dispositivo como no conforme | Inmediatamente | De forma predeterminada, la directiva está configurada para marcar el dispositivo como no conforme. Hay otras acciones disponibles. Para más información, consulte [Configuración de acciones para dispositivos no compatibles en Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Restricciones de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| General | Captura de pantalla | No configurado ||
| General | Cámara | No configurado ||
| General | Directiva de permisos predeterminada | Valor predeterminado del dispositivo ||
| General | Cambios de fecha y hora | No configurado ||
| General | Cambios de volumen | No configurado ||
| General | Restablecimiento de fábrica | Bloquear ||
| General | Arranque seguro | Bloquear ||
| General | Barra de estado | No configurado ||
| General | Servicios de datos de itinerancia | No configurado ||
| General | Cambios en la configuración de Wi-Fi | No configurado ||
| General | Configuración de Bluetooth | No configurado ||
| General | Tethering y acceso a los puntos de conexión | No configurado ||
| General | Almacenamiento USB | No configurado ||
| General | Bloquear transferencia de archivos USB | Bloquear ||
| General | Medios externos | Bloquear ||
| General | Datos de haz mediante NFC | No configurado ||
| General | Características de depuración | No configurado ||
| General | Ajuste del micrófono | No configurado ||
| General | Correos electrónicos de protección frente al restablecimiento de fábrica | No configurado ||
| General | Trampilla de escape de red | No configurado ||
| General | Actualización del sistema | Automático ||
| General | Ventanas de notificación | No configurado ||
| General | Omitir sugerencias al usar por primera vez | No configurado ||
| Seguridad del sistema | Examen de amenazas en las aplicaciones |Requerir ||
| Experiencia del dispositivo | Tipo de perfil de inscripción | Totalmente administrado ||
| Experiencia del dispositivo | Make Microsoft Launcher the default launcher (Hacer que Microsoft Launcher sea el iniciador predeterminado) | No configurado | Las organizaciones pueden optar por implementar Microsoft Launcher para garantizar una experiencia de pantalla principal coherente en los dispositivos totalmente administrados. Para más información, consulte [Cómo configurar Microsoft Launcher en dispositivos totalmente administrados de Android Enterprise con Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134). |
| Contraseña | Deshabilitar la pantalla de bloqueo | No configurado ||
| Contraseña | Características deshabilitadas en la pantalla de bloqueo | 0 servicios seleccionados ||
| Contraseña | Tipo de contraseña obligatoria | Numérica compleja ||
| Contraseña | Longitud mínima de la contraseña | 6 ||
| Contraseña | Número de días hasta que expire la contraseña | No configurado ||
| Contraseña | Número de contraseñas requeridas antes de que el usuario pueda reusar una | No configurado ||
| Contraseña | Número de errores de inicio de sesión antes de borrar el dispositivo | 10 ||
| Configuración de energía | Tiempo antes de que se bloquee la pantalla | 5 ||
| Configuración de energía | Pantalla activada mientras el dispositivo está conectado | No configurado ||
| Usuarios y cuentas | Agregar nuevos usuarios | No configurado ||
| Usuarios y cuentas | Bloquear la eliminación de usuarios | No configurado ||
| Usuarios y cuentas | Cambios de cuenta (solo dispositivos dedicados) | No configurado ||
| Usuarios y cuentas | Cuentas personales de Google | No configurado ||
| Usuarios y cuentas | El usuario puede configurar las credenciales | Bloquear ||
| Aplicaciones | Permitir la instalación desde orígenes desconocidos | No configurado ||
| Aplicaciones | Permitir el acceso a todas las aplicaciones en Google Play Store | No configurado | De forma predeterminada, los usuarios no pueden instalar aplicaciones personales desde Google Play Store en dispositivos totalmente administrados. Si las organizaciones quieren permitir que los dispositivos totalmente administrados se destinen a uso personal, considere la posibilidad de cambiar esta opción. |
| Aplicaciones | Actualizaciones automáticas de aplicación | Solo Wi-Fi | Las organizaciones deben ajustar esta opción de configuración según sus necesidades, ya que pueden producirse cargos por el plan de datos en caso de tener lugar actualizaciones de aplicaciones a través de la red de telefonía móvil. |

## <a name="fully-managed-enhanced-security"></a>Seguridad mejorada totalmente administrada

El nivel 2 es la configuración recomendada para los dispositivos corporativos en los que los usuarios acceden a información más confidencial. Estos dispositivos son un objetivo natural en las empresas de hoy en día. Se supone que con esta configuración no es necesario contar con un cuantioso personal con conocimientos de seguridad. Por lo tanto, será accesible para la mayoría de las organizaciones empresariales. Esta configuración amplía la configuración de nivel 1 con el establecimiento de directivas de contraseña más seguras y la deshabilitación de las funcionalidades de usuario o cuenta.

La configuración de nivel 2 incluye todas las configuraciones de directivas recomendadas para el nivel 1. Sin embargo, la configuración que se muestra a continuación incluye solo los valores que se han agregado o cambiado. Esta configuración puede tener un efecto algo mayor en los usuarios o en las aplicaciones. Aplica un nivel de seguridad más adecuado para los riesgos a los que se enfrentan los usuarios con acceso a información confidencial en los dispositivos móviles.

### <a name="device-compliance"></a>Cumplimiento de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| Seguridad del sistema | Número de días hasta que expire la contraseña | 365 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Seguridad del sistema |    Número de contraseñas requeridas antes de que el usuario pueda reusar una | 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |

### <a name="device-restrictions"></a>Restricciones de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| General | Correos electrónicos de protección frente al restablecimiento de fábrica | Direcciones de correo electrónico de la cuenta de Google ||
| General | Lista de direcciones de correo electrónico (solo la opción de direcciones de correo electrónico de la cuenta de Google) | example@gmail.com | Actualice manualmente esta directiva para especificar las direcciones de correo electrónico de Google de los administradores de dispositivos que pueden desbloquear los dispositivos después de que se eliminen. |
| Contraseña del dispositivo | Número de días hasta que expire la contraseña | 365 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Contraseña del dispositivo | Número de contraseñas requeridas antes de que el usuario pueda reusar una | 5 | Es posible que las organizaciones tengan que actualizar esta configuración para que coincida con su directiva de contraseñas. |
| Contraseña del dispositivo | Número de errores de inicio de sesión antes de borrar el dispositivo | 5 ||
| Usuarios y cuentas | Agregar nuevos usuarios | Bloquear ||
| Usuarios y cuentas | Bloquear la eliminación de usuarios | Bloquear ||
| Usuarios y cuentas | Cuentas personales de Google | Bloquear ||

## <a name="fully-managed-high-security"></a>Alta seguridad totalmente administrada

El nivel 3 es la configuración recomendada para:
- organizaciones con estructuras de seguridad grandes y sofisticadas.
- usuarios y grupos específicos a los que se dirigirán en exclusiva los adversarios.
Normalmente, tales organizaciones son el destino de adversarios sofisticados y con una buena financiación. Por lo tanto, reciben las restricciones y los controles adicionales que se enumeran a continuación.

Esta configuración amplía el nivel 2 de las siguientes maneras:
- aumenta la versión mínima del sistema operativo.
- garantiza que el dispositivo es compatible, puesto que aplica el nivel más seguro de defensa frente a amenazas para dispositivos móviles o de ATP de Microsoft Defender.
- aumenta la versión mínima del sistema operativo.
- aplica restricciones de dispositivo adicionales (por ejemplo, deshabilitar las notificaciones no censuradas en la pantalla de bloqueo).
- exige que las aplicaciones estén siempre actualizadas. 

La configuración de directiva que se aplica en el nivel 3 incluye todas las configuraciones de directivas recomendadas para el nivel 2. Los valores que se muestran a continuación incluyen solo los que se han agregado o cambiado. Esta configuración puede tener un efecto importante en los usuarios o las aplicaciones. Aplica un nivel de seguridad más adecuado para los riesgos a los que se enfrentan las organizaciones de destino.


### <a name="device-compliance"></a>Cumplimiento de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| ATP de Microsoft Defender | Solicitar que el dispositivo tenga o esté por debajo de la puntuación de riesgo de la máquina | Borrar | Esta configuración requiere ATP de Microsoft Defender. Para más información, consulte la aplicación del cumplimiento de [ATP de Microsoft Defender con acceso condicional en Intune](../protect/advanced-threat-protection.md).<p> Los clientes deben considerar la posibilidad de implementar ATP de Microsoft Defender o una solución de defensa contra frente a amenazas para dispositivos móviles. No es necesario implementar ambas. |
| Estado del dispositivo | Requerir que el dispositivo tenga el nivel de amenaza del dispositivo | Protegido | Esta configuración requiere un producto de defensa frente a amenazas para dispositivos móviles. Para más información, consulte [Mobile Threat Defense para dispositivos inscritos](../protect/mtd-device-compliance-policy-create.md).<p>Los clientes deben considerar la posibilidad de implementar ATP de Microsoft Defender o una solución de defensa contra frente a amenazas para dispositivos móviles. No es necesario implementar ambas.|
| Propiedades de dispositivos | Versión de SO mínima | Formato: Principal.Secundaria<br>Ejemplo: 10.0| Microsoft recomienda configurar la versión principal mínima de Android para que coincida con las versiones de Android compatibles con las aplicaciones de Microsoft. Los OEM y los dispositivos que se adhieren a los requisitos recomendados de Android Enterprise deben ser compatibles con la versión de publicación actual y una actualización posterior. Actualmente, Android recomienda Android 8.0 y versiones posteriores para los profesionales que trabajan con datos. Consulte Requisitos de Android Enterprise Recommended para conocer las recomendaciones más recientes de Android. |

### <a name="device-restrictions"></a>Restricciones de dispositivos

| Sección | Setting | Valor | Notas |
| ----- | ----- | ----- | ----- |
| General | Cambios de fecha y hora | Bloquear ||
| General | Tethering y acceso a los puntos de conexión | Bloquear ||
| General | Datos de haz mediante NFC | Bloquear ||
| Contraseña del dispositivo | Características deshabilitadas en la pantalla de bloqueo | Agentes de confianza, notificaciones no censuradas ||
| Aplicaciones | Actualizaciones automáticas de aplicación | Siempre | Las organizaciones deben ajustar esta opción de configuración según sus necesidades, ya que pueden producirse cargos por el plan de datos en caso de tener lugar actualizaciones de aplicaciones a través de la red de telefonía móvil. |


## <a name="next-steps"></a>Pasos siguientes

Los administradores pueden incorporar los niveles de configuración anteriores dentro de su metodología de implementación en anillo para su uso en producción y pruebas mediante la importación de las [plantillas JSON del marco de configuración de seguridad de Android Enterprise](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) de ejemplo con [scripts de PowerShell de Intune](https://github.com/microsoftgraph/powershell-intune-samples).
