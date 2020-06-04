---
title: Creación de perfiles de dispositivo en Microsoft Intune - Azure | Microsoft Docs
description: Agregue o configure un perfil de configuración de dispositivo en Microsoft Intune. Seleccione el tipo de plataforma, ajuste la configuración y agregue una etiqueta de ámbito.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74e365e50d73bb14f20376c92b43061b12d00003
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988470"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>Creación de un perfil de dispositivo en Microsoft Intune

Los perfiles de dispositivo le permiten agregar y ajustar configuraciones y, luego, insertar esas configuraciones en dispositivos de su organización. El artículo [Aplicación de la configuración y características en dispositivos con perfiles de dispositivos Microsoft Intune](device-profiles.md) entra en más detalles, incluido lo que puede hacer el usuario.

En este artículo:

- Se enumeran los pasos para crear un perfil.
- Se muestra cómo agregar una etiqueta de ámbito para "filtrar" el perfil.
- Describe las reglas de aplicabilidad en dispositivos Windows 10 y muestra cómo crear una regla.
- Se enumeran los tiempos de ciclo de actualización de sincronización cuando los dispositivos reciben perfiles y cualquier actualización de perfil.

## <a name="create-the-profile"></a>Creación del perfil

Los perfiles se crean en el [Centro de administración de Microsoft Endpoint Manager Intune](https://go.microsoft.com/fwlink/?linkid=2109431). En este Centro de administración, seleccione **Dispositivos**. Dispone de las siguientes opciones:

- **Información general**: muestra el estado de los perfiles y proporciona detalles adicionales sobre los perfiles que ha asignado a usuarios y dispositivos.
- **Supervisión**: compruebe si el estado de un perfil es correcto o erróneo, y consulte registros sobre los perfiles.
- **Por plataforma**: cree y vea directivas y perfiles en su plataforma. Esta vista también puede mostrar características específicas de la plataforma. Por ejemplo, seleccione **Windows**. Verá características específicas de Windows tales como **Anillos de actualización de Windows 10** y **Scripts de PowerShell**.
- **Directiva**: cree perfiles de dispositivo, cargue [scripts de PowerShell](../apps/intune-management-extension.md) personalizados para ejecutarlos en los dispositivos y agregue planes de datos a los dispositivos con [eSIM](esim-device-configuration.md).

Cuando cree un perfil (**Perfiles de configuración** > **Crear perfil**), elija la plataforma:

- **Administrador de dispositivos Android**
- **Android Enterprise**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 y versiones posteriores**
- **Windows 8.1 y versiones posteriores**
- **Windows Phone 8.1**

A continuación, elija el tipo de perfil. En función de la plataforma que haya elegido, las opciones que pueda configurar serán diferentes. En los artículos siguientes se describen las opciones de los distintos tipos de perfil:

- [Plantillas administrativas (Windows)](administrative-templates-windows.md)
- [Personalizado](custom-settings-configure.md)
- [Optimización de distribución (Windows)](delivery-optimization-windows.md)
- [Credencial derivada (Android Enterprise, iOS y iPadOS)](../protect/derived-credentials.md)
- [Características del dispositivo (macOS, iOS y iPadOS)](device-features-configure.md)
- [Firmware del dispositivo (Windows)](device-firmware-configuration-interface-windows.md)
- [Restricciones de dispositivos](device-restrictions-configure.md)
- [Unión a un dominio (Windows)](domain-join-configure.md)
- [Actualización de edición y conmutador de modo (Windows)](edition-upgrade-configure-windows-10.md)
- [Educación (iOS y iPadOS)](../fundamentals/education-settings-configure-ios.md)
- [Correo electrónico](email-settings-configure.md)
- [Endpoint Protection (macOS y Windows)](../protect/endpoint-protection-configure.md)
- [Extensiones (macOS)](kernel-extensions-overview-macos.md)
- [Identity Protection (Windows)](../protect/identity-protection-configure.md)
- [Quiosco](kiosk-settings.md)
- [ATP de Microsoft Defender (Windows)](../protect/advanced-threat-protection.md)
- [Perfil de Mobility Extensions (MX) (Administrador de dispositivos Android)](android-zebra-mx-overview.md)
- [OEMConfig (Android Enterprise)](android-oem-configuration-overview.md)
- [Certificado PKCS](../protect/certficates-pfx-configure.md)
- [Certificado PKCS importado](../protect/certificates-imported-pfx-configure.md)
- [Archivo de preferencias (macOS)](preference-file-settings-macos.md)
- [Certificado SCEP](../protect/certificates-scep-configure.md)
- [Evaluación segura (Education) (Windows)](education-settings-configure.md)
- [Dispositivo multiusuario compartido (Windows)](shared-user-device-settings.md)
- [Gastos de telecomunicaciones (Administrador de dispositivos Android, iOS y iPadOS)](telecom-expenses-monitor.md)
- [Certificado de confianza](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)

Por ejemplo, si selecciona **iOS/iPadOS** como plataforma, las opciones de perfil serán similares al perfil siguiente:

:::image type="content" source="./media/device-profile-create/create-device-profile.png" alt-text="Cree un perfil de iOS/iPadOS en Microsoft Intune.":::

## <a name="scope-tags"></a>Etiquetas de ámbito

Una vez que agrega la configuración, también puede agregar una etiqueta de ámbito al perfil. Las etiquetas de ámbito filtran los perfiles a grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Además, se usan en TI distribuida.

Para más información sobre las etiquetas de ámbito y lo que puede hacer el usuario, consulte el artículo sobre [el uso de RBAC y las etiquetas de ámbito para TI distribuida](../fundamentals/scope-tags.md).

## <a name="applicability-rules"></a>Reglas de aplicabilidad

Se aplica a:

- Windows 10 y versiones posteriores

Las reglas de aplicabilidad permiten a los administradores dirigirse a los dispositivos de un grupo que cumplen criterios específicos. Por ejemplo, se crea un perfil de restricciones de dispositivos que se aplica al grupo **Todos los dispositivos Windows 10**. Además, solo desea que el perfil esté asignado a los dispositivos que ejecutan Windows 10 Enterprise.

Para realizar esta tarea, cree una **regla de aplicabilidad**. Estas reglas son útiles para los escenarios siguientes:

- Utiliza Windows 10 Education (EDU). En Bellow College, desea dirigirse a todos los dispositivos Windows 10 EDU entre RS3 y RS4.
- Quiere dirigirse a todos los usuarios de recursos humanos en Contoso, pero solo desea dispositivos Windows 10 Professional o Enterprise.

Para abordar estos escenarios, puede:

- Crear un grupo de dispositivos que incluya todos los dispositivos de Bellows College. En el perfil, agregue una regla de aplicabilidad para que se aplique si la versión mínima del sistema operativo es `16299` y la versión máxima es `17134`. Asigne este perfil al grupo de dispositivos de Bellows College.

  Cuando se asigna, el perfil se aplica a los dispositivos entre las versiones mínima y máxima que especifique. En el caso de los dispositivos que no están entre las versiones mínima y máxima que especifique, su estado se muestra como **No aplicable**.

- Crear un grupo de usuarios que incluya a todos los usuarios de recursos humanos (RR  HH.) en Contoso. En el perfil, agregue una regla de aplicabilidad para que se aplique a los dispositivos que ejecutan Windows 10 Professional o Enterprise. Asigne este perfil al grupo usuarios de Recursos Humanos.

  Cuando se asigna, el perfil se aplica a los dispositivos que ejecutan Windows 10 Professional o Enterprise. En el caso de los dispositivos que no ejecutan estas ediciones, su estado se muestra como **No aplicable**.

- Si hay dos perfiles con la misma configuración exacta, se aplica el perfil sin una regla de aplicabilidad. 

  Por ejemplo, el perfil A tiene como destino el grupo de dispositivos de Windows 10, habilita BitLocker y no tiene una regla de aplicabilidad. El perfil B tiene como destino el mismo grupo de dispositivos de Windows 10, habilita BitLocker y tiene una regla de aplicabilidad para aplicar solo el perfil a Windows 10 Enterprise.

  Cuando se asignan ambos perfiles, se aplica el perfil A porque no tiene una regla de aplicabilidad. 

Al asignar el perfil a los grupos, las reglas de aplicabilidad actúan como un filtro y solo se dirigen a los dispositivos que cumplen los criterios.

### <a name="add-a-rule"></a>Agregar una regla

1. Seleccione **Reglas de aplicabilidad**. Puede elegir la**Regla** y la **Propiedad**:

    :::image type="content" source="./media/device-profile-create/applicability-rules.png" alt-text="Adición de una regla de aplicabilidad a un perfil de configuración de dispositivo Windows 10 en Microsoft Intune.":::

2. En **Regla**, elija si desea incluir o excluir usuarios o grupos. Las opciones son:

    - **Asignar perfil si**: incluye usuarios o grupos que cumplen los criterios especificados.
    - **No asignar perfil si**: excluye los usuarios o grupos que cumplen los criterios especificados.

3. En **Propiedad**, elija el filtro. Las opciones son: 

    - **Edición del SO**: en la lista, compruebe las ediciones de Windows 10 que quiere incluir (o excluir) en la regla.
    - **Versión del SO**: escriba los números de versión **min** y **max** de Windows 10 que quiere incluir (o excluir) en la regla. Ambos valores son necesarios.

      Por ejemplo, puede especificar `10.0.16299.0` (RS3 o 1709) para la versión mínima y `10.0.17134.0` (RS4 o 1803) para la versión máxima. O bien, puede ser más específico e indicar `10.0.16299.001` para la versión mínima y `10.0.17134.319` para la versión máxima.

4. Haga clic en **Agregar** para guardar los cambios.

## <a name="refresh-cycle-times"></a>Tiempos de ciclo de actualización

Intune usa diferentes ciclos de actualización para comprobar si hay actualizaciones para los perfiles de configuración. Si el dispositivo se inscribió recientemente, la inserción en el repositorio se ejecuta con más frecuencia. En el artículo sobre [ciclos de actualización de directivas y perfiles](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) se muestran los tiempos de actualización estimados.

En cualquier momento, los usuarios pueden abrir la aplicación Portal de empresa de Intune y sincronizar el dispositivo para comprobar de inmediato las actualizaciones del perfil.

## <a name="recommendations"></a>Recomendaciones

Al crear perfiles, tenga en cuenta las siguientes recomendaciones:

- Asigne un nombre a las directivas para saber lo que son y lo que hacen. Todas las [directivas de cumplimiento](../protect/create-compliance-policy.md) y [perfiles de configuración](../configuration/device-profile-create.md) tienen una propiedad **Descripción** opcional. En **Descripción**, sea concreto e incluya información que permita que otros usuarios sepan lo que hace la directiva.

  Algunos ejemplos de perfil de configuración incluyen:

  **Nombre del perfil**: plantilla de administración: perfil de configuración de OneDrive para todos los usuarios de Windows 10  
  **Descripción de perfil**: perfil de plantilla de administración de OneDrive que incluye la configuración mínima y base para todos los usuarios de Windows 10. Lo ha creado user@contoso.com para impedir que los usuarios compartan datos de la organización con cuentas personales de OneDrive.

  **Nombre del perfil**: perfil de VPN de todos los usuarios de iOS/iPadOS  
  **Descripción de perfil**: perfil de VPN que incluye la configuración mínima y base para que todos los usuarios de iOS/iPadOS se conecten a la VPN de Contoso. Lo ha creado user@contoso.com para que los usuarios se autentiquen automáticamente en la VPN, en lugar de solicitarles su nombre de usuario y contraseña.

- Cree el perfil por su tarea, como configurar las opciones de Microsoft Edge, habilitar la configuración antivirus de Microsoft Defender, bloquear dispositivos con jailbreak de iOS/iPadOS, etc.

- Cree perfiles que se apliquen a grupos específicos, como Marketing, Ventas, Administradores de TI, o por ubicación o sistema educativo.

- Separe las directivas de usuario de las directivas de dispositivo.

  Por ejemplo, las [plantillas administrativas en Intune](administrative-templates-windows.md) tienen miles de valores de configuración de ADMX. Estas plantillas muestran si se aplica una opción de configuración a usuarios o dispositivos. Al crear plantillas de administración, asigne la configuración de usuario a un grupo de usuarios y la configuración de dispositivo a un grupo de dispositivos.

  En la imagen siguiente se muestra un ejemplo de un valor de configuración que se puede aplicar a los usuarios o a los dispositivos:

  :::image type="content" source="./media/device-profile-create/setting-applies-to-user-and-device.png" alt-text="Plantilla de administración de Intune que se aplica a usuarios y dispositivos.":::

- Cada vez que cree una directiva restrictiva, comunique este cambios a los usuarios. Por ejemplo, si va a cambiar el requisito de código de acceso de 4 a 6 caracteres, informe a los usuarios antes de asignar la directiva.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).
