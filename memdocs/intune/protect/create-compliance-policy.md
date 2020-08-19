---
title: Creación de directivas de cumplimiento de dispositivos en Microsoft Intune - Azure | Microsoft Docs
description: Creación de directivas de cumplimiento de dispositivos, información general de los estados y los niveles de gravedad, uso del estado En período de gracia, trabajar con el acceso condicional, control de los dispositivos sin una directiva asignada y diferencias de cumplimiento en Azure Portal y el portal clásico en Microsoft Intune
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
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c1431105bdba9731bda4599e310889bfbf86a2c
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252261"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Creación de una directiva de cumplimiento en Microsoft Intune

Las directivas de cumplimiento de dispositivos son una característica clave cuando se usa Intune para proteger los recursos de su organización. En Intune, puede crear reglas y opciones de configuración que los dispositivos deben cumplir para que se consideren conformes, por ejemplo, una versión de SO mínima. Si el dispositivo no las cumple, puede bloquear el acceso a datos y recursos mediante el [acceso condicional](conditional-access.md).

También puede realizar acciones en caso de incumplimiento, como enviar un correo electrónico de notificación al usuario. Para información general sobre lo que hacen las directivas de cumplimiento y cómo se usan, consulte [Introducción al cumplimiento de dispositivos](device-compliance-get-started.md).

En este artículo:

- Se enumeran los requisitos previos y los pasos para crear una directiva de cumplimiento.
- Se muestra cómo asignar la directiva a los grupos de dispositivos y usuarios.
- Se describen características adicionales, como las etiquetas de ámbito para "filtrar" las directivas, y los pasos que puede realizar en los dispositivos que no cumplen con las reglamentaciones.
- Se enumeran los tiempos de ciclo de actualización de sincronización cuando los dispositivos reciben actualizaciones de directiva.

## <a name="before-you-begin"></a>Antes de comenzar

Para usar las directivas de cumplimiento de dispositivos, asegúrese de lo siguiente:

- Use las siguientes suscripciones:

  - Intune
  - Si usa el acceso condicional, necesita la edición Azure Active Directory (AD) Premium. [Precios de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) muestra lo que obtiene con las distintas ediciones. El cumplimiento de Intune no requiere Azure AD.

- Use una plataforma compatible:

  - Administrador de dispositivos Android
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1

- Inscriba dispositivos en Intune (necesario para ver el estado de cumplimiento)

- Inscriba dispositivos en un usuario o realice la inscripción sin un usuario primario. Los dispositivos inscritos en varios usuarios no se admiten.

## <a name="create-the-policy"></a>Creación de la directiva

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Directivas de cumplimiento** > **Directivas** > **Crear directiva**.

3. Selecciona una **plataforma** para esta directiva de entre las siguientes opciones:
   - *Administrador de dispositivos Android*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows 8.1 y versiones posteriores*
   - *Windows 10 y versiones posteriores*

    Para *Android Enterprise*, también seleccionará un **tipo de directiva**:
     - *Directiva de Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado de Android*
     - *Directiva de cumplimiento del perfil de trabajo Android*

    Luego, seleccione **Crear** para abrir la ventana de configuración **Crear directiva**.

4. En la pestaña **Aspectos básicos**, rellene el campo **Nombre** para que le ayude a identificarla más tarde. Por ejemplo, un buen nombre de directiva es **Marcar los dispositivos iOS/iPadOS con jailbreak como no compatibles**.

   También puede especificar una descripción en **Descripción**.
  
5. En la pestaña **Configuración de cumplimiento**, expanda las categorías disponibles y configure las opciones de la directiva.  En los siguientes artículos se describen los valores de configuración de cada plataforma:
   - [Administrador de dispositivos Android](compliance-policy-create-android.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows 8.1 y versiones posteriores](compliance-policy-create-windows-8-1.md)
   - [Windows 10 y versiones posteriores](compliance-policy-create-windows.md)  

6. En la pestaña **Ubicaciones**, puede forzar el cumplimiento según la ubicación del dispositivo. Elija entre las ubicaciones existentes. Si aún no tiene una ubicación disponible, consulte [Usar ubicaciones (límite de red)](use-network-locations.md) para obtener instrucciones.
   > [!TIP]
   > Las **ubicaciones** solo están disponibles para la plataforma de *administrador de dispositivos Android*.

7. En la pestaña **Acciones de no cumplimiento**, especifique una secuencia de acciones que se aplicarán automáticamente a los dispositivos que no satisfagan esta directiva de cumplimiento.

   Puede agregar varias acciones y configurar programaciones y detalles adicionales para algunas de ellas. Por ejemplo, puede cambiar la programación de la acción predeterminada *Marcar el dispositivo como no conforme* para que se produzca después de un día. Luego, puede agregar una acción para enviar un correo electrónico al usuario cuando el dispositivo no sea compatible para advertir de ese estado. También puede agregar acciones que bloqueen o retiren dispositivos que no sean compatibles.

   Para información sobre las acciones que se pueden configurar, consulte [Adición de acciones para dispositivos no compatibles](actions-for-noncompliance.md), donde se habla también de cómo crear correos electrónicos de notificación para enviarlos a los usuarios.

   Otro ejemplo incluye el uso de ubicaciones en las que se agrega al menos una ubicación a una directiva de cumplimiento. En este caso, la acción predeterminada en caso de no cumplimiento se aplica cuando se selecciona al menos una ubicación. Si el dispositivo no está conectado a ninguna de las ubicaciones seleccionadas, se considera no compatible. Puede configurar la programación para dar a los usuarios un período de gracia, por ejemplo, un día.

8. En la pestaña **Etiquetas de ámbito**, seleccione etiquetas para filtrar las directivas por grupos concretos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Una vez que agrega la configuración, también puede agregar una etiqueta de ámbito a las directivas de cumplimiento. 

   Para información sobre el uso de etiquetas de ámbito, consulte [Uso de etiquetas de ámbito para filtrar directivas](../fundamentals/scope-tags.md).

9. En la pestaña **Asignaciones**, asigne la directiva a los grupos.  

   Seleccione **+ Seleccionar grupos para incluir** y, luego, asigne la directiva a uno o varios grupos. La directiva se aplicará a estos grupos cuando la guarde después del siguiente paso. 

10. En la pestaña **Revisar + crear**, revise la configuración y seleccione **Crear** cuando esté listo para guardar la directiva de cumplimiento.  

    Los usuarios o dispositivos de destino de la directiva se evalúan para comprobar su cumplimiento cuando se registran en Intune.

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>Tiempos de ciclo de actualización

Intune usa distintos ciclos de actualización para comprobar las actualizaciones de las directivas de cumplimiento. Si el dispositivo se inscribió recientemente, la inserción en el repositorio se ejecuta con más frecuencia. En el artículo sobre [ciclos de actualización de directivas y perfiles](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) se muestran los tiempos de actualización estimados.

En cualquier momento, los usuarios pueden abrir la aplicación Portal de empresa de Intune y sincronizar el dispositivo para comprobar de inmediato las actualizaciones del perfil.

### <a name="assign-an-ingraceperiod-status"></a>Asignar un estado En período de gracia

El estado En período de gracia de una directiva de cumplimiento es un valor. Este valor se determina mediante la combinación del período de gracia de un dispositivo y el estado real del dispositivo para esa directiva de cumplimiento.

En concreto, si un dispositivo tiene un estado No conforme para una directiva de cumplimiento asignada y si se dan los casos siguientes:

- El dispositivo no tiene asignado ningún período de gracia, de modo que el valor asignado para la directiva de cumplimiento es No conforme.
- El dispositivo tiene un período de gracia que ha expirado, de modo que el valor asignado para la directiva de cumplimiento es No conforme.
- El dispositivo tiene un período de gracia futuro, de modo que el valor asignado para la directiva de cumplimiento es En período de gracia

En la siguiente tabla se resumen estos aspectos:

|Estado de cumplimiento real|Valor del período de gracia asignado|Estado de cumplimiento efectivo|
|---------|---------|---------|
|No conforme |Ningún periodo de gracia asignado |No conforme |
|No conforme |Fecha de ayer|No conforme|
|No conforme |Fecha de mañana|En período de gracia|

Para obtener más información sobre la supervisión de las directivas de cumplimiento de dispositivos, vea [Supervisión de las directivas de cumplimiento de dispositivos Intune](compliance-policy-monitor.md).

### <a name="assign-a-resulting-compliance-policy-status"></a>Asignar un estado de directiva de cumplimiento resultante

Si un dispositivo tiene varias directivas de cumplimiento y distintos estados de cumplimiento para dos o más de dichas directivas, se asigna un único estado de cumplimiento resultante. Esta asignación se basa en un nivel de gravedad conceptual que se asigna a cada estado de cumplimiento. Cada estado de cumplimiento tiene el nivel de gravedad siguiente:

|Estado  |Gravedad  |
|---------|---------|
|Unknown     |1|
|No aplicable     |2|
|conforme|3|
|En período de gracia|4|
|No conforme|5|
|Error|6|

Si un dispositivo tiene varias directivas de cumplimiento, se le asignará el nivel de gravedad más alto de todas las directivas.

Por ejemplo, un dispositivo tiene 3 directivas de cumplimiento asignadas: la primera, con el estado Desconocido (gravedad 1); la segunda, con el estado Conforme (gravedad 3) y, la tercera, con el estado InGracePeriod (gravedad 4). El estado InGracePeriod tiene el nivel de gravedad más alto. Por lo tanto, las tres directivas tienen el estado de cumplimiento InGracePeriod.

## <a name="next-steps"></a>Pasos siguientes

[Supervise las directivas](compliance-policy-monitor.md).
