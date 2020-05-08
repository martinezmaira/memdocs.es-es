---
title: Configuración de cumplimiento de dispositivos Android en Microsoft Intune - Azure | Microsoft Docs
description: Vea una lista de todas las opciones que puede usar al configurar el cumplimiento de dispositivos Android en Microsoft Intune. Configure reglas de contraseña, elija una versión mínima o máxima de sistema operativo, restrinja aplicaciones específicas, evite reutilizar contraseñas y mucho más.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f8cb75907befaa747ebae1718815d9722ff7085
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729225"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Configuración de Android para marcar dispositivos como compatibles o no compatibles con Intune

En este artículo se enumeran y describen las distintas opciones de configuración de cumplimiento que se pueden establecer en dispositivos con Android y versiones posteriores en Intune. Como parte de la solución de administración de dispositivos móviles (MDM), use estas opciones para marcar los dispositivos liberados (descodificados) como no compatibles, establecer un nivel de amenaza permitido, habilitar Google Play Protect y mucho más.

Esta característica se aplica a:

- Administrador de dispositivos Android

Como administrador del servicio Intune, use esta configuración de cumplimiento para proteger mejor los recursos de la organización. Para más información sobre las directivas de cumplimiento y lo que hacen, vea [Introducción a las directivas de cumplimiento](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Antes de comenzar

[Crear una directiva de cumplimiento](create-compliance-policy.md#create-the-policy). En **Plataforma**, seleccione **Administrador de dispositivos Android**.

## <a name="microsoft-defender-atp"></a>ATP de Microsoft Defender

- **Solicitar que el dispositivo tenga o esté por debajo de la puntuación de riesgo de la máquina**  

  Seleccione la puntuación de riesgo de la máquina máxima permitida para los dispositivos evaluados por ATP de Microsoft Defender. Los dispositivos que superan esta puntuación se marcan como no compatibles.
  - **Sin configurar** (*valor predeterminado*).
  - **Borrar**
  - **Baja**
  - **Media**
  - **Alta**

## <a name="device-health"></a>Estado del dispositivo

- **Dispositivos administrados con el administrador de dispositivos**  
  Las funcionalidades del *administrador de dispositivos* se han sustituido por Android Enterprise.

  - **Sin configurar** (*valor predeterminado*).
  - **Bloquear**: al bloquear el administrador de dispositivos, se guiará a los usuarios para que cambien a la administración de perfiles de trabajo de Android Enterprise con el fin de recuperar el acceso.

- **Dispositivos con acceso "root"**  
  Se impide que los dispositivos con acceso "root" tengan acceso corporativo. (Esta comprobación de cumplimiento se admite para Android 4.0 y versiones posteriores).

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Bloquear**: marcar los dispositivos raíz (con jailbreak) como no conformes.

- **Requerir que el dispositivo tenga el nivel de amenaza del dispositivo**  
  Use este valor de configuración para hacer que la evaluación del riesgo de un servicio Mobile Threat Defense sea una condición para el cumplimiento.

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Protegido**: esta opción es la más segura y el dispositivo no puede tener ninguna amenaza. Si se detecta cualquier nivel de amenaza en el dispositivo, se evaluará como no conforme.
  - **Bajo**: el dispositivo se evalúa como conforme si solo hay amenazas de nivel bajo. Cualquier valor por encima coloca al dispositivo en un estado de no conformidad.
  - **Medio:** el dispositivo se evalúa como compatible si las amenazas existentes en él son de nivel bajo o medio. Si se detecta que el dispositivo tiene amenazas de nivel alto, se determina como no conforme.
  - **Alto**: esta opción es la menos segura, ya que permite todos los niveles de amenaza. Quizás sea útil si utiliza esta solución solo con fines informativos.

### <a name="google-play-protect"></a>Google Play Protect

- **Google Play Services está configurado**  
  Google Play Services permite actualizaciones de seguridad y es una dependencia de nivel base para muchas características de seguridad en los dispositivos de Google certificados.

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.  
  - **Requerir**: se requiere que la aplicación Google Play Services esté instalada y habilitada.  

- **Proveedor de seguridad actualizada**

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Requerir**: se requiere que un proveedor de seguridad actualizado pueda proteger un dispositivo frente a vulnerabilidades conocidas.

- **Examen de amenazas en las aplicaciones**

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Requerir**: se requiere que la característica **Verificar aplicaciones** de Android esté habilitada.

  > [!NOTE]
  > En la plataforma Android heredada, esta característica es una configuración de cumplimiento. Intune solo puede comprobar si esta configuración está habilitada en el nivel de dispositivo.

- **Atestación de dispositivo SafetyNet**  
  especifique el nivel de [atestación de SafetyNet](https://developer.android.com/training/safetynet/attestation.html) que se debe cumplir. Las opciones son:

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Comprobar integridad básica**
  - **Comprobar integridad básica y dispositivos certificados**

> [!NOTE]
> Para configurar las opciones de Google Play Protect mediante directivas de protección de aplicaciones, vea [Configuración de directivas de protección de aplicaciones de Intune](../apps/app-protection-policy-settings-android.md#conditional-launch) en Android.

## <a name="device-properties"></a>Propiedades de dispositivos

### <a name="operating-system-version"></a>Versión de sistema operativo

- **Versión de SO mínima**  
  cuando un dispositivo no cumple el requisito de versión mínima del sistema operativo, se notifica como no conforme. Se muestra un vínculo con información sobre cómo actualizar el sistema. El usuario final puede optar por actualizar el dispositivo y luego acceder a los recursos de la empresa.

  *De forma predeterminada, no se configura ninguna versión*.

- **Versión de SO máxima**  
  cuando un dispositivo usa una versión de SO posterior a la de la especificada en la regla, se bloquea el acceso a los recursos de la empresa. Se solicita al usuario que se ponga en contacto con el administrador de TI. Mientras no se cambie la regla para permitir la versión de SO, el dispositivo no podrá acceder a los recursos de la empresa.

  *De forma predeterminada, no se configura ninguna versión*.

## <a name="system-security"></a>Seguridad del sistema

### <a name="password"></a>Contraseña

- **Requerir una contraseña para desbloquear dispositivos móviles**  
  *Compatible con Android 4.0 y versiones posteriores, o KNOX 4.0 y versiones posteriores.*

  Esta configuración especifica si es preciso que los usuarios escriban una contraseña para poder acceder a información en sus dispositivos móviles. Valor recomendado: Requerir  

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Requerir**: los usuarios deben introducir una contraseña para poder acceder al dispositivo.

- **Tipo de contraseña requerida**  
  *Compatible con Android 4.0 y versiones posteriores, o KNOX 4.0 y versiones posteriores.*

  elija si una contraseña debe incluir solo caracteres numéricos o una combinación de números y otros caracteres.

  - **Valor predeterminado del dispositivo**: para evaluar el cumplimiento de las contraseñas, asegúrese de seleccionar una más sólida, distinta a la **predeterminada del dispositivo**.
  - **Biométrico de seguridad baja**
  - **Al menos numérica**
  - **Numérica compleja**: no se permiten números consecutivos ni repetidos (como `1111` o `1234`).
  - **Al menos alfabética**
  - **Al menos alfanumérica**
  - **Al menos alfanumérica con símbolos**

  En función de la configuración de este valor, una o varias de las opciones siguientes están disponibles:

  - **Longitud mínima de la contraseña**  
    *Compatible con Android 4.0 y versiones posteriores, o KNOX 4.0 y versiones posteriores.*

    Escriba el número mínimo de dígitos o caracteres que debe tener la contraseña del usuario.

  - **Máximo de minutos de inactividad antes de solicitar la contraseña**  
    *Compatible con Android 4.0 y versiones posteriores, o KNOX 4.0 y versiones posteriores.*

    especifique el tiempo de inactividad antes de que el usuario deba volver a escribir la contraseña. Si elige **Sin configurar** (valor predeterminado), no se evalúa el cumplimiento o incumplimiento de esta configuración.

  - **Número de días hasta que expire la contraseña**  
  *Compatible con Android 4.0 y versiones posteriores, o KNOX 4.0 y versiones posteriores.*

  Seleccione el número de días que faltan para que expire la contraseña y el usuario deba crear otra.

  - **Número de contraseñas anteriores que no se pueden reutilizar**  
    indique el número de contraseñas recientes que no se pueden volver a usar. Utilice esta configuración para impedir que el usuario cree contraseñas usadas anteriormente. (Compatible con Android 4.0 y versiones posteriores, o bien KNOX 4.0 y versiones posteriores).

### <a name="encryption"></a>Cifrado

- **Cifrado de almacenamiento de datos en un dispositivo**  
  *Compatible con Android 4.0 y versiones posteriores, o KNOX 4.0 y versiones posteriores.*

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Requerir**: se cifra el almacenamiento de datos en los dispositivos. Los dispositivos se cifran al elegir la opción **Requerir una contraseña para desbloquear dispositivos móviles**.

### <a name="device-security"></a>Seguridad de dispositivos

- **Bloquear aplicaciones de orígenes desconocidos**  
  *Compatible de Android 4.0 a Android 7.x. No se admite en Android 8.0 y versiones posteriores*

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Bloquear**: bloquee los dispositivos con orígenes habilitados mediante **Seguridad > Orígenes desconocidos** (*se admite en Android 4.0 y hasta Android 7.x.; no se admite en Android 8.0 y versiones posteriores*).

  Para realizar instalaciones de prueba de las aplicaciones, se deben permitir los orígenes desconocidos. Si no realiza instalaciones de prueba de las aplicaciones Android, establezca esta característica en **Bloquear** para habilitar esta directiva de cumplimiento.

  > [!IMPORTANT]
  > Las aplicaciones de instalación de prueba requieren que se habilite la opción **Bloquear aplicaciones de orígenes desconocidos**. Aplique esta directiva de cumplimiento solo si no realiza instalaciones de prueba de las aplicaciones Android en dispositivos.

- **Integridad en tiempo de ejecución de la aplicación Portal de empresa**
  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Requerir**: elija *Requerir* para confirmar que la aplicación Portal de empresa cumple los siguientes requisitos:

    - Tiene instalado el entorno de tiempo de ejecución predeterminado.
    - Está firmada correctamente.
    - No se encuentra en modo de depuración.
    - Se ha instalado desde un origen conocido.

- **Bloquear depuración USB en el dispositivo**  
  *(Compatible con Android 4.2 y versiones posteriores)*

  - **Sin configurar** (*valor predeterminado*): no se evalúa el cumplimiento o incumplimiento de esta opción de configuración.
  - **Bloquear**: evita que los dispositivos usen la característica de depuración USB.

- **Nivel mínimo de revisión de seguridad**  
  *(Compatible con Android 6.0 y versiones posteriores)*

  seleccione el nivel de revisión de seguridad más antiguo que puede tener un dispositivo. Los dispositivos que no estén al menos en este nivel de revisión se consideran no conformes. La fecha debe especificarse en el formato `YYYY-MM-DD`.

  *De forma predeterminada, no se configura ninguna fecha*.

- **Aplicaciones restringidas**  
  escriba la información pertinente en **Nombre de la aplicación** e **Identificador de lote de aplicaciones** para las aplicaciones que deben estar restringidas y luego seleccione **Agregar**. Un dispositivo con al menos una aplicación restringida instalada se marca como no conforme.

## <a name="next-steps"></a>Pasos siguientes

- [Agregar acciones para dispositivos no compatibles](actions-for-noncompliance.md) y [usar etiquetas de ámbito para filtrar directivas](../fundamentals/scope-tags.md).
- [Supervisar las directivas de cumplimiento](compliance-policy-monitor.md).
- Vea [Configuración de directivas de cumplimiento para dispositivos Android Enterprise](compliance-policy-create-android-for-work.md).
