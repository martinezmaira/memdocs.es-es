---
title: Configuración de ATP de Microsoft Defender en Microsoft Intune - Azure | Microsoft Docs
description: Configure Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) en Intune, incluida la conexión a ATP, la incorporación de dispositivos, la asignación del cumplimiento de los niveles de riesgo y las directivas de acceso condicional.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/12/2020
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
ms.openlocfilehash: ad02078d2a8b9926de463e01d3dcbc675c721e4a
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179526"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>Configuración de ATP de Microsoft Defender en Intune

La información y los procedimientos de este artículo le ayudarán a configurar la integración de ATP de Microsoft Defender con Intune. La configuración incluye los siguientes pasos generales:

- Habilitación de ATP de Microsoft Defender para su inquilino
- Incorporación de dispositivos que ejecutan Windows y Android
- Uso de directivas de cumplimiento para establecer los niveles de riesgo del dispositivo
- Uso de directivas de acceso condicional para bloquear los dispositivos que superan los niveles de riesgo esperados

Antes de comenzar, el entorno debe cumplir los [requisitos previos](../protect/advanced-threat-protection.md#prerequisites) para usar ATP de Microsoft Defender con Intune.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Habilitación de ATP de Microsoft Defender en Intune

El primer paso que debe realizar es configurar la conexión de servicio a servicio entre Intune y ATP de Microsoft Defender. Para ello es necesario acceso administrativo al Centro de seguridad de Microsoft Defender y a Intune.

Solo tiene que habilitar ATP de Microsoft Defender una vez por inquilino.

### <a name="to-enable-microsoft-defender-atp"></a>Para habilitar ATP de Microsoft Defender

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Endpoint security** (Seguridad del punto de conexión)  > **ATP de Microsoft Defender** y, luego, seleccione **Abrir el Centro de seguridad de Microsoft Defender**.

   ![Seleccionar para abrir el Centro de seguridad de Microsoft Defender](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. En el **Centro de seguridad de Microsoft Defender**, siga estos pasos:
   1. Seleccione **Configuración** > **Características avanzadas**.
   2. Para **Microsoft Intune connection** (Conexión con Intune), elija **Activado**:

      ![Habilitar la conexión a Intune](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

   3. Seleccione **Guardar preferencias**.

4. Vuelva a **ATP de Microsoft Defender** en el Centro de administración de Microsoft Endpoint Manager. En **Configuración de la directiva de cumplimiento de MDM**, en función de las necesidades de su organización, haga lo siguiente:
   - Establezca **Conectar dispositivos Windows de la versión 10.0.15063 y posteriores a ATP de Microsoft Defender** en **Activado**.
   - Establezca **Conectar dispositivos Android de la versión 6.0.0 y posteriores a ATP de Microsoft Defender** en **Activado**.

5. Seleccione **Guardar**.

> [!TIP]
> Al integrar una nueva aplicación en Intune Mobile Threat Defense y habilitar la conexión con Intune, este servicio crea una directiva de acceso condicional clásica en Azure Active Directory. Todas las aplicaciones de MTD que integre, incluido [ATP de Microsoft Defender](advanced-threat-protection.md) o cualquiera de nuestros [asociados de MTD](mobile-threat-defense.md#mobile-threat-defense-partners) adicionales, crean una directiva de acceso condicional clásica. Estas directivas se pueden omitir, pero no se deben editar, eliminar ni deshabilitar.
>
> Si se elimina la directiva clásica, deberá eliminar la conexión a Intune que era responsable de su creación y, a continuación, configurarla de nuevo. Esto vuelve a crear la directiva clásica. No se admite la migración de directivas clásicas para aplicaciones de MTD al nuevo tipo de directiva para el acceso condicional.
>
> Directivas de acceso condicional clásicas para aplicaciones de MTD:
>
> - Las usa Intune MTD para requerir que los dispositivos estén registrados en Azure AD, de modo que dispongan de un id. de dispositivo antes de comunicarse con los asociados de MTD. El id. es necesario para que los dispositivos puedan informar de su estado correctamente a Intune.
> - No tiene ningún efecto en otros recursos o aplicaciones en la nube.
> - Son diferentes a las directivas de acceso condicional que puede crear para ayudarle con la administración de MTD.
> - No interactúan de forma predeterminada con otras directivas de acceso condicional usadas para la evaluación.
>
> Para ver las directivas de acceso condicional clásicas, en [Azure](https://portal.azure.com/#home), vaya a **Azure Active Directory** > **Acceso condicional** > **Directivas clásicas**.

## <a name="onboard-devices"></a>Incorporación de dispositivos

Cuando se habilita la compatibilidad con ATP de Microsoft Defender en Intune, se establece una conexión de servicio a servicio entre Intune y ATP de Microsoft Defender. Después, puede incorporar dispositivos administrados con Intune a ATP de Microsoft Defender, lo que permite la recopilación de datos sobre los niveles de riesgo de los dispositivos.

### <a name="onboard-windows-devices"></a>Incorporación de dispositivos Windows

Cuando estableció la conexión entre Intune y ATP de Microsoft Defender, Intune recibió un paquete de configuración de incorporación de ATP de Microsoft Defender procedente de ATP de Microsoft Defender. Este paquete de configuración se implementa en los dispositivos Windows con un perfil de configuración de dispositivo para ATP de Microsoft Defender.

El paquete de configuración configura los dispositivos para que se comuniquen con los [servicios de ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) para examinar archivos y detectar amenazas. El dispositivo también está configurado para notificar a ATP de Microsoft Defender el nivel de riesgo de los dispositivos en función de las directivas de cumplimiento que cree.

Después de incorporar un dispositivo mediante el paquete de configuración, no es necesario hacerlo de nuevo. También puede incorporar dispositivos mediante una [directiva de grupo o Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>Creación del perfil de configuración de dispositivos para incorporar dispositivos Windows

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. En **Plataforma**, seleccione **Windows 10 y versiones posteriores**.
4. En **Tipo de perfil**, seleccione **ATP de Microsoft Defender (Windows 10 Desktop)** y, luego, elija **Crear**.
5. En la página **Aspectos básicos**, rellene los campos *Nombre* y *Descripción* (opcional) del perfil y, luego, elija **Siguiente**.
6. En la página **Opciones de configuración**, configure lo siguiente:

   - **Tipo de paquete de configuración del cliente ATP de Microsoft Defender**: seleccione **Incorporar** para agregar el paquete de configuración al perfil. Seleccione **Cesar** para quitar el paquete de configuración del perfil.
  
     > [!NOTE]
     > Si ha establecido correctamente una conexión con ATP de Microsoft Defender, Intune **incorporará** automáticamente el perfil de configuración, mientras que la configuración **Tipo de paquete de configuración del cliente ATP de Microsoft Defender** no estará disponible.
  
   - **Uso compartido de muestras para todos los archivos**: la opción **Habilitar** permite recopilar muestras y compartirlas con ATP de Microsoft Defender. Por ejemplo, si ve un archivo sospechoso, puede enviarlo a ATP de Microsoft Defender para un análisis profundo. **No configurado**: no se comparte ninguna muestra con ATP de Microsoft Defender.
   - **Frecuencia de informes de telemetría urgentes**: para los dispositivos que presentan un riesgo alto, **habilite** esta opción para informar de la telemetría al servicio de ATP de Microsoft Defender con más frecuencia.

     [Incorporar máquinas Windows 10 con Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) tiene más detalles sobre estas configuraciones de ATP de Microsoft Defender.

7. Seleccione **Siguiente** para abrir la página **Etiquetas de ámbito**. Las etiquetas de ámbito son opcionales. Seleccione **Siguiente** para continuar.

8. En la página **Asignaciones**, seleccione los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

   Seleccione **Siguiente**.

9. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**. El nuevo perfil se muestra en la lista cuando se selecciona el tipo de directiva del perfil creado.
 Seleccione **Aceptar** y, luego, **Crear** para guardar los cambios y crear el perfil.

### <a name="onboard-android-devices"></a>Incorporación de dispositivos Android

Después de establecer la conexión de servicio a servicio entre Intune y ATP de Microsoft Defender, puede incorporar dispositivos Android a ATP de Microsoft Defender. La incorporación configura los dispositivos para que se comuniquen con ATP de Microsoft Defender, que luego recopila datos sobre el nivel de riesgo de los dispositivos.

A diferencia de los dispositivos Windows, no hay un paquete de configuración para los dispositivos que ejecutan Android. En su lugar, consulte [Introducción a ATP de Microsoft Defender para Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) en la documentación de ATP de Microsoft Defender para ver los requisitos previos y las instrucciones de incorporación para Android.

En el caso de los dispositivos que ejecutan Android, también puede usar la directiva de Intune para modificar ATP de Microsoft Defender en Android. Para obtener más información, consulte [Protección web de ATP de Microsoft Defender](../protect/advanced-threat-protection-manage-android.md).

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>Creación y asignación de una directiva de cumplimiento para establecer el nivel de riesgo del dispositivo

Para los dispositivos Windows y Android, la directiva de cumplimiento determina el nivel de riesgo que se considera aceptable para un dispositivo.

Si no está familiarizado con la creación de una directiva de cumplimiento, consulte el procedimiento [Creación de la directiva](../protect/create-compliance-policy.md#create-the-policy) del artículo *Creación de una directiva de cumplimiento en Microsoft Intune*. La siguiente información es específica de la configuración de ATP de Microsoft Defender como parte de una directiva de cumplimiento.

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Directivas de cumplimiento** > **Directivas** > **Crear directiva**.

3. Para **Plataforma**, use el cuadro desplegable para seleccionar una de las opciones siguientes:
   - **Windows 10 y versiones posteriores**
   - **Administrador de dispositivos Android**
   - **Android Enterprise**

   Luego, seleccione **Crear** para abrir la ventana de configuración **Crear directiva**.

4. Rellene el campo **Nombre** para que le ayude a identificar esta directiva más tarde. También puede especificar una descripción en **Descripción**.
  
5. En la pestaña **Configuración de compatibilidad**, expanda el grupo **ATP de Microsoft Defender** y establezca la opción **Solicitar que el dispositivo tenga o esté por debajo de la puntuación de riesgo de la máquina** en su nivel preferido.

   Las clasificaciones de nivel de amenaza vienen [determinadas por ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Borrar**: este nivel es el más seguro. El dispositivo no puede tener ninguna amenaza existente y aún puede acceder a los recursos de la empresa. Si se encuentra alguna amenaza, el dispositivo se clasificará como no conforme. (ATP de Microsoft Defender usa el valor *Seguro*).
   - **Bajo**: el dispositivo se evalúa como compatible si solo hay amenazas de nivel bajo. Los dispositivos con niveles de amenaza medio o alto no son compatibles.
   - **Media**: el dispositivo se evalúa como compatible si las amenazas que se encuentran en él son de nivel bajo o medio. Si se detectan amenazas de nivel alto, se determinará que el dispositivo no es compatible.
   - **Alta**: este nivel es el menos seguro, ya que permite todos los niveles de amenaza. Los dispositivos con niveles de amenaza alto, medio o bajo se consideran compatibles.

6. Complete la configuración de la directiva, incluida la asignación de esta a los grupos correspondientes.


## <a name="create-a-conditional-access-policy"></a>Creación de una directiva de acceso condicional

Las directivas de acceso condicional pueden usar datos de ATP de Microsoft Defender para bloquear el acceso a los recursos de los dispositivos que superan el nivel de amenaza establecido. Puede bloquear el acceso del dispositivo a los recursos corporativos, como SharePoint o Exchange Online.

> [!TIP]
> Acceso condicional es una tecnología de Azure Active Directory (Azure AD). El nodo *Acceso condicional* que se encuentra en el Centro de administración de Microsoft Endpoint Manager es el mismo nodo que el de *Azure AD*.

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Endpoint security** (Seguridad del punto de conexión)  > **Acceso condicional** > **Nueva directiva**.

3. En **Nombre**, escriba un nombre de directiva y seleccione **Usuarios y grupos**. Utilice las opciones Incluir o Excluir para agregar los grupos para la directiva y seleccione **Listo**.

4. Seleccione **Aplicaciones en la nube** y elija las aplicaciones que desea proteger. Por ejemplo, elija **Seleccionar aplicaciones** y seleccione **Office 365 SharePoint Online** y **Office 365 Exchange Online**.

   Haga clic en **Listo** para guardar los cambios.

5. Seleccione **Condiciones** > **Aplicaciones cliente** para aplicar la directiva a las aplicaciones y los exploradores. Por ejemplo, seleccione **Sí** y habilite **Explorador** y **Aplicaciones móviles y aplicaciones de escritorio**.

   Haga clic en **Listo** para guardar los cambios.

6. Seleccione **Conceder** para aplicar el acceso condicional basado en el cumplimiento del dispositivo. Por ejemplo, seleccione **Conceder acceso** > **requieren que el dispositivo se marquen como compatibles**.

    Elija **Seleccionar** para guardar los cambios.

7. Seleccione **Habilitar directiva** y luego **crear** para guardar los cambios.

## <a name="next-steps"></a>Pasos siguientes

- [Configuración de ATP de Microsoft Defender en Android](../protect/advanced-threat-protection-manage-android.md)
- [Supervisión del cumplimiento de los niveles de riesgo](../protect/advanced-threat-protection-monitor.md)

Obtenga más información en la documentación de Intune:

- [Uso de tareas de seguridad con la administración de vulnerabilidades de ATP para corregir problemas de los dispositivos](atp-manage-vulnerabilities.md)
- [Introducción a las directivas de cumplimiento de dispositivos de Intune](device-compliance-get-started.md)

Obtenga más información en la documentación de ATP de Microsoft Defender:

- [Acceso condicional de ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Panel de riesgo de ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
