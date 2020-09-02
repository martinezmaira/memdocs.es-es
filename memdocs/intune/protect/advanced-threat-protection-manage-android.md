---
title: Administración de la protección web de ATP de Microsoft Defender para dispositivos Android en Microsoft Intune - Azure | Microsoft Docs
description: Configuración de la protección web de Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) para Android en Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49423d1d1b887aaf3ed3323ff36678bb7319b1ad
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909472"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>Configuración de ATP de Microsoft Defender en dispositivos Android administrados con Intune

Al integrar Microsoft Intune y Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender), puede usar los perfiles de configuración de dispositivos para modificar algunas opciones de configuración de ATP de Microsoft Defender en dispositivos Android.

Antes de lo anterior, debe [configurar correctamente ATP de Microsoft Defender en Intune](../protect/advanced-threat-protection-configure.md) e incorporar dispositivos Android en ATP de Microsoft Defender.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Configuración de la protección web en dispositivos que ejecutan Android

De forma predeterminada, ATP de Microsoft Defender para Android incluye y habilita la característica de protección web. La [protección web](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) ayuda a proteger los dispositivos frente a las amenazas web y a los usuarios frente a ataques de suplantación de identidad.

Aunque está habilitada de forma predeterminada, hay razones válidas para deshabilitar esta protección en algunos dispositivos Android. Por ejemplo, puede optar por usar solo la característica de examen de aplicaciones de ATP de Microsoft Defender o por impedir que la protección web use la VPN mientras examina las direcciones URL dañinas.

Intune permite desactivar parcial o totalmente la característica de protección web. El método que use y las capacidades que pueda deshabilitar dependerán de cómo se inscriba el dispositivo Android con Intune:

- **Administrador de dispositivos Android**: use un perfil de configuración con el fin de establecer la configuración de OMA-URI personalizada en el dispositivo para deshabilitar toda la característica de protección web o solo el uso de VPN. Para obtener información general sobre la configuración personalizada de dispositivos Android, consulte [Configuración personalizada](../configuration/custom-settings-android.md).

- **Perfil de trabajo de Android Enterprise**: use un perfil de configuración de aplicaciones y el *diseñador de configuración* para deshabilitar la protección web. Este tipo de método e inscripción permite deshabilitar todas las funciones de protección web, pero no permite deshabilitar solo el uso de VPN. Para obtener información general sobre las directivas de configuración de aplicaciones, vea [Uso del diseñador de configuración](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

Para configurar la protección web en los dispositivos, use los procedimientos siguientes con el fin de crear e implementar la configuración aplicable.

### <a name="disable-web-protection-for-android-device-administrator"></a>Deshabilitación de la protección web para el administrador de dispositivos Android

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. Escriba los valores siguientes:

   - **Plataforma**: Seleccione **Administrador de dispositivos Android**.
   - **Perfil**: seleccione **Personalizado**

   Seleccione **Crear**.

4. En **Datos básicos**, escriba la siguiente información:

   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, *Perfil personalizado de Android para la protección web de ATP de Microsoft Defender*.
   - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional, pero se recomienda aplicarla.

5. En **Opciones de configuración**, seleccione **Agregar**.

   Especifique las opciones de la configuración que quiere implementar:

   - **Deshabilitar la protección web**:
     - **Nombre**: escriba un nombre único para esta configuración OMA-URI, de modo que pueda encontrarla fácilmente. Por ejemplo, *Deshabilitar la protección web de ATP de Microsoft Defender*.
     - **Descripción**: (opcional) escriba una descripción con información general sobre la configuración y otros detalles importantes.
     - **OMA-URI**: escriba **./Vendor/MSFT/DefenderATP/AntiPhishing**.
     - **Tipo de datos**: use la lista desplegable y seleccione **Entero**.
     - **Valor**: escriba **0** para deshabilitar la protección web, incluido el examen basado en VPN.
       > [!NOTE]
       > Escriba **1** para habilitar la protección web, que es el valor predeterminado.

   - **Deshabilitar solo el uso de la VPN de protección web**:
     - **Nombre**: escriba un nombre único para esta configuración OMA-URI, de modo que pueda encontrarla fácilmente. Por ejemplo, *Deshabilitar la VPN de protección web de ATP de Microsoft Defender*.
     - **Descripción**: (opcional) escriba una descripción con información general sobre la configuración y otros detalles importantes.
     - **OMA-URI**: escriba **./Vendor/MSFT/DefenderATP/Vpn**.
     - **Tipo de datos**: use la lista desplegable y seleccione **Entero**.
     - **Valor**: escriba **0** para deshabilitar el examen basado en VPN.
       > [!NOTE]
       > Escriba **1** para habilitar la protección web, que es el valor predeterminado.

   Seleccione **Agregar** para guardar la configuración de OMA-URI y, luego, haga clic en **Siguiente** para continuar.

6. En **Asignaciones**, especifique los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

7. Cuando haya terminado, elija **Crear** en **Revisar y crear**. El nuevo perfil se muestra en la lista cuando se selecciona el tipo de directiva del perfil creado.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Deshabilitación de la protección web para el perfil de trabajo de Android Enterprise

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** y haga clic en Dispositivos administrados.

3. En **Datos básicos**, escriba la siguiente información:

   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, *Configuración de aplicaciones Android para la protección web de ATP de Microsoft Defender*.
   - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional, pero se recomienda aplicarla.
   - **Plataforma**: seleccione **Android Enterprise**.
   - **Tipo de perfil**: seleccione **Solo perfil de trabajo**.
   - **Aplicación de destino**: haga clic en **Seleccionar aplicación**.

4. En **Aplicación asociada**, busque y seleccione **ATP de Microsoft Defender** y haga clic en **Aceptar** > **Siguiente**.

5. En **Configuración**, use el desplegable **Formato de opciones de configuración**, seleccione **Usar diseñador de configuraciones** y haga clic en **Agregar**. Se abrirá el editor de JSON.

6. Busque y seleccione **Protección web** y haga clic en **Aceptar** para volver a la página **Configuración**.

7. En **Valor de configuración**, escriba **0** para deshabilitar la protección web.

   > [!NOTE]
   > Escriba **1** para habilitar la protección web, que es el valor predeterminado.

   Seleccione **Siguiente** para continuar.

8. En **Asignaciones**, especifique los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

9. Cuando haya terminado, elija **Crear** en **Revisar y crear**. El nuevo perfil se muestra en la lista cuando se selecciona el tipo de directiva del perfil creado.

## <a name="next-steps"></a>Pasos siguientes

- [Supervisión del cumplimiento de los niveles de riesgo](../protect/advanced-threat-protection-monitor.md)
- [Uso de tareas de seguridad con la administración de vulnerabilidades de ATP para corregir problemas de los dispositivos](../protect/atp-manage-vulnerabilities.md).

Obtenga más información en la documentación de ATP de Microsoft Defender:

- [Acceso condicional de ATP de Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Panel de riesgo de ATP de Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)