---
title: Integración de Windows Hello para empresas con Microsoft Intune
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo crear una directiva para controlar el uso de Windows Hello para empresas en dispositivos administrados durante la inscripción de dispositivos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: 7088bfd5b27d986e12a175de1bdea0bf060c3ad3
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252527"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>Integración de Windows Hello para empresas con Microsoft Intune  

Puede integrar Windows Hello para empresas (anteriormente Microsoft Passport for Work) con Microsoft Intune durante la inscripción de dispositivos.

Hello para empresas es un método alternativo de inicio de sesión que usa Active Directory o una cuenta de Azure Active Directory para reemplazar una contraseña, tarjeta inteligente o tarjeta inteligente virtual. Permite usar un *gesto de usuario* para iniciar sesión, en lugar de una contraseña. Un gesto de usuario podría ser una autenticación biométrica con un PIN, como Windows Hello, o un dispositivo externo como un lector de huellas digitales.

Intune se integra con Hello para empresas de dos maneras:

- **Todo el inquilino** (*este artículo)* : Se puede crear una directiva de Intune en *Inscripción de dispositivos*. Esta directiva se destina a toda la organización (a todos los inquilinos). Es compatible con la configuración rápida (OOBE) de Windows AutoPilot y se aplica cuando se inscribe un dispositivo.
- **Grupos discretos**: En el caso de los dispositivos que se hayan inscrito previamente con Intune, use un perfil de [**Identity Protection**](../protect/identity-protection-configure.md) de configuración de dispositivo para configurar dispositivos para Windows Hello para empresas. Los perfiles de Identity Protection pueden dirigirse a usuarios o dispositivos asignados y aplicarse durante la sincronización.

Además, Intune admite los siguientes tipos de directivas para administrar algunas opciones de configuración de Windows Hello para empresas:

- [**Líneas de base de seguridad**](../protect/security-baselines.md). Las siguientes líneas de base incluyen la configuración de Windows Hello para empresas:
  - [Configuración de línea de base de Advanced Threat Protection de Microsoft Defender](../protect/security-baseline-settings-defender-atp.md#windows-hello-for-business)
  - [Configuración de línea de base de seguridad de MDM de Windows](../protect/security-baseline-settings-mdm-all.md#windows-hello-for-business)
- Directiva de seguridad para los puntos de conexión para la [**protección de cuentas**](../protect/endpoint-security-account-protection-policy.md). Vea la [configuración de protección de cuentas](../protect/endpoint-security-account-protection-profile-settings.md#account-protection).

El resto de este artículo se centra en la creación de una directiva de Windows Hello para empresas predeterminada destinada a toda la organización.

> [!IMPORTANT]
> Antes de la Actualización de aniversario, se podían establecer dos PIN diferentes para autenticarse en los recursos:
>
> - El **PIN de dispositivo** se usaba para desbloquear el dispositivo y conectarse a recursos de nube.
> - El **PIN de trabajo** se usaba para acceder a recursos de Azure AD en los dispositivos personales del usuario (BYOD).
>
> En la Actualización de aniversario, estos dos PIN se combinaron en un solo PIN de dispositivo.
> Las directivas de configuración de Intune que establezca para controlar el PIN de dispositivo y las directivas de Windows Hello para empresas que configure serán las que establecerán ahora este nuevo valor de PIN.
> Si ha establecido ambos tipos de directivas para controlar el PIN, se aplica la directiva de Windows Hello para empresas.
> Para garantizar que se resuelven los conflictos de directivas y que la directiva de PIN se aplica correctamente, actualice su directiva de Windows Hello para empresas de modo que coincida con la configuración de la directiva de configuración y pídales a los usuarios que sincronicen sus dispositivos en la aplicación del portal de empresa.

## <a name="create-a-windows-hello-for-business-policy"></a>Crear una directiva de Windows Hello para empresas

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vaya a **Dispositivos** >  **Inscripción** > **Inscribir dispositivos** > **Inscripción de Windows** > **Windows Hello para empresas**. Se abre el panel de Windows Hello para empresas.

3. En **Configurar Windows Hello para empresas**, seleccione entre las opciones siguientes.

   - **Habilitado**. Seleccione esta opción si quiere configurar Windows Hello para empresas.  Cuando se selecciona *Habilitado*, los otros valores de configuración de Windows Hello se vuelven visibles y se pueden configurar para los dispositivos.

   - **Deshabilitado**. Si no quiere habilitar Windows Hello para empresas durante la inscripción de los dispositivos, seleccione esta opción. Cuando está deshabilitada, los usuarios no pueden aprovisionar Windows Hello para empresas. Cuando está establecido en *Deshabilitado*, las opciones siguientes pueden configurarse igualmente para Windows Hello para empresas, aunque esta directiva no habilite Windows Hello para empresas.

   - **No configurado**. Seleccione esta opción si no quiere usar Intune para controlar la configuración de Windows Hello para empresas. No se cambia ninguna de las opciones de configuración de Windows Hello para empresas existentes en los dispositivos Windows 10. Todas las demás configuraciones del panel no están disponibles.

4. Si ha seleccionado **Habilitado** en el paso anterior, configure las opciones necesarias que se aplican a todos los dispositivos Windows 10 inscritos. Después de configurar estos valores, seleccione **Guardar**.

   - **Usar un Módulo de plataforma segura (TPM)** :

     Un chip de TPM ofrece una capa adicional de seguridad de datos. Elija uno de los siguientes valores:

     - **Requerido** (valor predeterminado). Solo los dispositivos que tengan un TPM accesible pueden aprovisionar Windows Hello para empresas.
     - **Preferido**. Los dispositivos intentan primero usar un TPM. Si esta opción no está disponible, pueden usar el cifrado de software.

   - **Longitud mínima de PIN** y **Longitud máxima de PIN**:

     Configura los dispositivos para que usen las longitudes de PIN mínima y máxima que se especifiquen, lo cual garantiza un inicio de sesión seguro. La longitud predeterminada del PIN es de seis caracteres, pero se puede aplicar una longitud mínima de cuatro. La longitud de PIN máxima es de 127 caracteres.

   - **Letras minúsculas en el PIN**, **Letras mayúsculas en el PIN** y **Caracteres especiales en el PIN**.

     Si quiere aplicar un PIN más seguro, puede requerir el uso de letras mayúsculas, letras minúsculas y caracteres especiales en el PIN. Para cada una, seleccione entre:

     - **Permitido**. Los usuarios pueden usar el tipo de carácter en el PIN, pero no es obligatorio.

     - **Requerido**. Los usuarios deben incluir al menos uno de los tipos de carácter en el PIN. Por ejemplo, una práctica habitual consiste en obligar a usar como mínimo una mayúscula y un carácter especial.

     - **No permitido** (valor predeterminado). Los usuarios no deben usar estos tipos de caracteres en el PIN. (Este es también el comportamiento si no se configura esta opción).

       Entre los caracteres especiales se incluyen los siguientes: **! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~**

   - **Expiración del PIN (días)** :

     Se recomienda especificar un período de expiración del PIN, transcurrido el cual hay que cambiarlo. El valor predeterminado es 41 días.

   - **Recordar historial de PIN**:

     Restringe la reutilización de los PIN usados anteriormente. De forma predeterminada, no se pueden volver a usar los últimos cinco PIN.

   - **Permitir autenticación biométrica**:

     Habilita la autenticación biométrica, como el reconocimiento facial o la huella digital, como alternativa a un PIN para Windows Hello para empresas. Los usuarios todavía deben configurar un PIN de trabajo por si produce un error en la autenticación biométrica. Elija de entre las siguientes opciones:

     - **Sí**. Windows Hello para empresas permite la autenticación biométrica.
     - **No**. Windows Hello para empresas impide la autenticación biométrica (en todos los tipos de cuenta).

   - **Usar tecnología mejorada de suplantación de identidad cuando esté disponible**:

     configura si se usan las características de protección contra la suplantación de identidad de Windows Hello en los dispositivos que las admitan. Por ejemplo, la detección de una fotografía de una cara en lugar de un rostro real.

     Cuando esta opción se establece en **Sí**, Windows exige que todos los usuarios usen tecnología contra la suplantación de identidad en características faciales cuando se admitan.

   - **Permitir inicio de sesión por teléfono**:

     Si esta opción se establece en **Sí**, los usuarios pueden usar una cuenta de Passport remota para que actúe como dispositivo complementario portátil para la autenticación del equipo de escritorio. El equipo de escritorio debe estar unido a Azure Active Directory y el dispositivo complementario debe configurarse con un PIN de Windows Hello para empresas.

## <a name="windows-holographic-for-business-support"></a>Compatibilidad con Windows Holographic for Business

Windows Holographic for Business es compatible con las siguientes opciones de configuración de Windows Hello para empresas:

- Usar un Módulo de plataforma segura (TPM)
- Longitud mínima del PIN
- Longitud máxima del PIN
- Minúsculas en el PIN
- Mayúsculas en el PIN
- Caracteres especiales en el PIN
- Expiración del PIN (días)
- Recordar historial de PIN

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre Windows Hello para empresas, consulte [la guía](https://technet.microsoft.com/library/mt589441.aspx) de la documentación de Windows 10.
