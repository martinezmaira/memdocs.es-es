---
title: Directivas de cumplimiento de dispositivos en Microsoft Intune - Azure | Microsoft Docs
description: Introducción al uso de directivas de cumplimiento, incluyendo la configuración de directivas de cumplimiento y las directivas de cumplimiento de dispositivos para Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/28/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 227a44436f4490c9b3e2188609a9714a0e842149
ms.sourcegitcommit: eb51bb38d484e8ef2ca3ae3c867561249fa413f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206322"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>Uso de directivas de cumplimiento para establecer reglas para los dispositivos que administra con Intune

Las soluciones de administración de dispositivos móviles (MDM) como Intune pueden ayudar a proteger los datos de la organización exigiendo a los usuarios y dispositivos que cumplan algunos requisitos. En Intune, esta característica se denomina *directivas de cumplimiento*.

Las directivas de cumplimiento en Intune:

- Definen las reglas y la configuración que los usuarios y los dispositivos deben cumplir para ser compatibles.
- Incluyen las acciones que se aplican a los dispositivos que no son compatibles. Las acciones en caso de no cumplimiento pueden alertar a los usuarios de las condiciones de no cumplimiento y proteger los datos en dispositivos no compatibles.
- Se pueden [combinar con el acceso condicional](#integrate-with-conditional-access), que luego puede bloquear a los usuarios y dispositivos que no cumplen las reglas.

Las directivas de cumplimiento de Intune tienen dos partes:

- **Configuración de directivas de cumplimiento**: la configuración para todo el inquilino que es similar a una directiva de cumplimiento integrada que cada dispositivo recibe. La configuración de directivas de cumplimiento establece una línea de base para el funcionamiento de la directiva de cumplimiento en el entorno de Intune, lo que incluye si los dispositivos que no han recibido directivas de cumplimiento de dispositivos son compatibles o no.

- **Directiva de cumplimiento de dispositivos**: reglas específicas de la plataforma que se configuran e implementan en grupos de usuarios o dispositivos.  Estas reglas definen los requisitos de los dispositivos, como los sistemas operativos mínimos o el uso del cifrado de discos. Los dispositivos deben cumplir estas reglas para que se consideren compatibles.

Al igual que otras directivas de Intune, las evaluaciones de las directivas de cumplimiento de un dispositivo dependen del momento en el que el dispositivo se sincroniza con Intune y los [ciclos de actualización de directivas y perfiles](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="compliance-policy-settings"></a>Configuración de directivas de cumplimiento

La *configuración de directivas de cumplimiento* es una configuración para todo el inquilino que determina cómo el servicio de cumplimiento de Intune interactúa con los dispositivos. Esta configuración es distinta de la que se configura en una directiva de cumplimiento de dispositivos.

Para administrar la configuración de directivas de cumplimiento, inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y vaya a **Seguridad de los puntos de conexión** > **Cumplimiento de dispositivos** > **Configuración de directivas de cumplimiento**.

La configuración de directivas de cumplimiento incluye las configuraciones siguientes:

- **Marcar los dispositivos que no tienen asignada una directiva de cumplimiento como**

  Esta configuración determina cómo Intune trata los dispositivos a los que no se ha asignado una directiva de cumplimiento de dispositivos. Esta configuración tiene dos valores:
  - **Compatible** (*valor predeterminado*): esta característica de seguridad está desactivada. Los dispositivos a los que no se les envía una directiva de cumplimiento de dispositivos se consideran *compatibles*.
  - **No compatible**: esta característica de seguridad está activada. Los dispositivos que no han recibido una directiva de cumplimiento de dispositivos se consideran no compatibles.

  Si usa el acceso condicional con las directivas de cumplimiento de dispositivos, se recomienda cambiar esta configuración a **No compatible** para asegurarse de que solo los dispositivos que se confirman como compatibles puedan tener acceso a los recursos.

  Si un usuario final no es compatible porque no se le ha asignado ninguna directiva, la [aplicación Portal de empresa](../apps/company-portal-app.md) muestra que no se han asignado directivas de cumplimiento.

- **Detección de jailbreak mejorada** (*se aplica solo a iOS/iPadOS*)

  Esta configuración solo funciona con dispositivos a los que se dirige una directiva de cumplimiento de dispositivos que bloquea los dispositivos con jailbreak.  (Consulte la configuración [Estado del dispositivo](compliance-policy-create-ios.md#device-health) para iOS/iPadOS).

  Esta configuración tiene dos valores:

  - **Deshabilitada** (*valor predeterminado*): esta característica de seguridad está desactivada. Esta configuración no tiene ningún efecto en los dispositivos que reciben la directiva de cumplimiento de dispositivos que bloquea los dispositivos con jailbreak.
  - **Habilitada**: esta característica de seguridad está activada. Los dispositivos que reciben la directiva de cumplimiento de dispositivos para bloquear los dispositivos con jailbreak usan la detección de jailbreak mejorada.

  Cuando se habilita en un dispositivo iOS/iPadOS aplicable, el dispositivo:

  - Habilita los servicios de ubicación en el nivel de sistema operativo.
  - Siempre permite que el Portal de empresa use los servicios de ubicación.
  - Utiliza sus servicios de ubicación para desencadenar la detección de jailbreak con mayor frecuencia en segundo plano. Intune no almacena los datos de ubicación del usuario.

  La detección de jailbreak mejorada ejecuta una evaluación cuando:

  - Se abre la aplicación Portal de empresa
  - El dispositivo se mueve físicamente una distancia significativa, que es aproximadamente 500 metros o más. Intune no puede garantizar que cada cambio de ubicación significativo genere una comprobación de detección de jailbreak, ya que esta comprobación depende de la conexión de red de un dispositivo en ese momento.

  En iOS 13 y versiones posteriores, esta característica requiere que los usuarios seleccionen *Permitir siempre* cada vez que el dispositivo les pida que sigan permitiendo al Portal de empresa usar su ubicación en segundo plano. Si los usuarios no permiten siempre el acceso a la ubicación y tienen configurada una directiva con esta opción, el dispositivo se marcará como no compatible.

- **Período de validez del estado de cumplimiento (días)**

  Especifique un período en el que los dispositivos deben notificar correctamente todas las directivas de cumplimiento recibidas. Si un dispositivo no puede informar su estado de cumplimiento con respecto a una directiva antes de que expire el período de validez, el dispositivo se considerará como no compatible.

  De manera predeterminada, el período se establece en 30 días. Puede configurar un período de entre 1 y 120 días.

  Puede ver los detalles sobre el cumplimiento del dispositivo con respecto a la configuración del período de validez. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y vaya a **Dispositivos** > **Supervisión** > **Configuración de cumplimiento**. Esta configuración tiene el nombre **Is active** (Activo) en la columna *Configuración*.  Para más información sobre esta vista de estado de cumplimiento y vistas de estados de cumplimiento relacionadas, consulte [Supervisión del cumplimiento de dispositivos](compliance-policy-monitor.md).

## <a name="device-compliance-policies"></a>Directivas de cumplimiento de dispositivos

Directivas de cumplimiento de dispositivos de Intune:

- Definen las reglas y la configuración que los usuarios y los dispositivos administrados deben cumplir para ser compatibles. Algunos ejemplos de reglas incluyen requerir que los dispositivos ejecuten una versión mínima del sistema operativo, que no tengan jailbreak ni acceso "root" y que tengan un *nivel de amenaza* según lo especificado en el software de administración de amenazas que ha integrado con Intune.
- Admiten acciones que se aplican a los dispositivos que no cumplen con las reglas de cumplimiento. Entre los ejemplos de acciones se incluyen el bloqueo remoto o el envío de un correo electrónico del usuario del dispositivo sobre el estado del dispositivo para poder corregirlo.
- Se implementan en los usuarios de grupos de usuarios o dispositivos de grupos de dispositivos. Cuando se implementa una directiva de cumplimiento en un usuario, se comprueba el cumplimiento de todos los dispositivos del usuario. El uso de grupos de dispositivos en este escenario ayuda con los informes de cumplimiento.

Si usa el acceso condicional, las directivas de acceso condicional pueden usar los resultados de cumplimiento de dispositivos para bloquear el acceso a los recursos desde dispositivos no compatibles.

La configuración disponible que puede especificar en una directiva de cumplimiento de dispositivos depende del tipo de plataforma que selecciona cuando crea una directiva. Las distintas plataformas de dispositivos admiten diferentes configuraciones y cada tipo de plataforma requiere una directiva independiente.  

Los temas siguientes se vinculan a artículos dedicados para distintos aspectos de la directiva de configuración de dispositivos.

- [**Acciones en caso de no cumplimiento**](actions-for-noncompliance.md): cada directiva de cumplimiento de dispositivos incluye una o varias acciones en caso de no cumplimiento. Estas acciones son reglas que se aplican a los dispositivos que no cumplen con las condiciones establecidas en la directiva.

  De manera predeterminada, cada directiva de cumplimiento de dispositivos incluye la acción para marcar un dispositivo como no compatible si no cumple con una regla de directiva. Después, la directiva aplica al dispositivo cualquier acción adicional en caso de no cumplimiento que se haya configurado, en función de las programaciones que establece para esas acciones.

  Las acciones en caso de no cumplimiento pueden ayudar a alertar a los usuarios cuando su dispositivo no es compatible o a proteger los datos que pueda haber en un dispositivo. Algunos ejemplos de acciones son:

  - El **envío de alertas por correo electrónico** a usuarios y grupos con detalles sobre el dispositivo no compatible. Puede configurar la directiva para enviar un correo electrónico inmediatamente después de que el dispositivo se marca como no conforme y, de nuevo, de manera periódica, hasta que el dispositivo sea compatible.
  - El **bloqueo remoto de dispositivos** que no son compatibles durante algún tiempo.
  - La **retirada de dispositivos**  si han sido no compatibles durante un tiempo. Esta acción quita el dispositivo de la administración de Intune y quita todos los datos de la empresa del dispositivo.

- [**Configuración de ubicaciones de red**](use-network-locations.md): compatibles con los dispositivos Android, puede configurar *ubicaciones de red* para luego usarlas como una regla de cumplimiento de dispositivos. Este tipo de regla puede marcar un dispositivo como no compatible cuando está fuera de una red especificada o cuando sale de una. Para poder especificar una regla de ubicación, debe configurar las ubicaciones de red.

- [**Creación de una directiva**](create-compliance-policy.md): con la información que aparece en este artículo, puede revisar los requisitos previos, examinar las opciones para configurar reglas, especificar acciones en caso de no cumplimiento y asignar la directiva a los grupos. En este artículo también se incluye información sobre los tiempos de actualización de directivas.

  Consulte la configuración de cumplimiento de dispositivos para las distintas plataformas de dispositivos:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 y versiones posteriores](compliance-policy-create-windows-8-1.md)
  - [Windows 10 y versiones posteriores](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>Supervisión del estado de cumplimiento

Intune incluye un panel de cumplimiento de dispositivos que se usa para supervisar el estado de cumplimiento de los dispositivos y para profundizar en las directivas y los dispositivos para saber más. Para más información sobre este panel, consulte [Supervisión del cumplimiento de dispositivos](compliance-policy-monitor.md).

## <a name="integrate-with-conditional-access"></a>Integración con el acceso condicional

Cuando usa el acceso condicional, puede configurar las directivas de acceso condicional para usar los resultados de las directivas de cumplimiento de dispositivos con el fin de determinar qué dispositivos pueden acceder a los recursos de la organización. Este control de acceso es aparte de las acciones en caso de no cumplimiento que se incluyen en las directivas de cumplimiento de dispositivos.

Cuando un dispositivo se inscribe en Intune, se registra en Azure AD. El estado de cumplimiento de los dispositivos se informa a Azure AD. Si las directivas de acceso condicional tienen controles de acceso establecidos en *Requerir que el dispositivo esté marcado como compatible*, el acceso condicional usa ese estado de cumplimiento para determinar si se debe conceder o bloquear el acceso al correo electrónico y a otros recursos de la organización.

Si va a utilizar el estado de cumplimiento de dispositivos con directivas de acceso condicional, revise cómo el inquilino ha configurado la opción *Marcar los dispositivos que no tienen asignada una directiva de cumplimiento como*, que se administra en [Configuración de directivas de cumplimiento](#compliance-policy-settings).

Para más información sobre cómo usar el acceso condicional con las directivas de cumplimiento de dispositivos, consulte [Acceso condicional basado en dispositivos](conditional-access-intune-common-ways-use.md#device-based-conditional-access).

Más información sobre el acceso condicional en la documentación de Azure AD:

- [¿Qué es el acceso condicional?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [¿Qué es una identidad de dispositivo?](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>Referencia para el no cumplimiento y acceso condicional en las distintas plataformas

En la tabla siguiente se describe cómo administrar la configuración de no conformidad cuando se usa una directiva de cumplimiento con una directiva de acceso condicional.

- **Corregido**: el sistema operativo del dispositivo exige compatibilidad. Por ejemplo, se obliga al usuario a establecer un PIN.

- **En cuarentena**: el sistema operativo del dispositivo no exige cumplimiento. Por ejemplo, los dispositivos Android y Android Enterprise no obligan al usuario a cifrar el dispositivo. Si el dispositivo no es conforme, se emprenden las acciones siguientes:
  - El dispositivo se bloquea si se aplica una directiva de acceso condicional al usuario.
  - La aplicación Portal de empresa de Intune notifica al usuario sobre cualquier problema de cumplimiento.

---------------------------

|**Configuración de directiva**| **Plataforma** |
| --- | ----|
| **Configuración de PIN o contraseña** | - **Android 4.0 y versiones posteriores**: En cuarentena<br>- **Samsung Knox Standard 4.0 y versiones posteriores**: En cuarentena<br>- **Android Enterprise**: En cuarentena  <br>  <br>- **iOS 8.0 y versiones posteriores**: Corregido<br>- **macOS 10.11 y versiones posteriores**: Corregido  <br>  <br>- **Windows 8.1 y versiones posteriores**: Corregido<br>- **Windows Phone 8.1 y versiones posteriores**: Corregido|
| **Cifrado del dispositivo** | - **Android 4.0 y versiones posteriores**: En cuarentena<br>- **Samsung Knox Standard 4.0 y versiones posteriores**: En cuarentena<br>- **Android Enterprise**: En cuarentena<br><br>- **iOS 8.0 y versiones posteriores**: Corregido (estableciendo PIN)<br>- **macOS 10.11 y versiones posteriores**: Corregido (estableciendo PIN)<br><br>- **Windows 8.1 y versiones posteriores**: No disponible<br>- **Windows Phone 8.1 y versiones posteriores**: Corregido |
| **Dispositivo liberado o modificado** | - **Android 4.0 y versiones posteriores**: En cuarentena (no es una configuración)<br>- **Samsung Knox Standard 4.0 y versiones posteriores**: En cuarentena (no es una configuración)<br>- **Android Enterprise**: En cuarentena (no es una configuración)<br><br>- **iOS 8.0 y versiones posteriores**: En cuarentena (no es una configuración)<br>- **macOS 10.11 y versiones posteriores**: No disponible<br><br>- **Windows 8.1 y versiones posteriores**: No disponible<br>- **Windows Phone 8.1 y versiones posteriores**: No disponible |
| **Perfil de correo electrónico** | - **Android 4.0 y versiones posteriores**: No disponible<br>- **Samsung Knox Standard 4.0 y versiones posteriores**: No disponible<br>- **Android Enterprise**: No disponible<br><br>- **iOS 8.0 y versiones posteriores**: En cuarentena<br>- **macOS 10.11 y versiones posteriores**: En cuarentena<br><br>- **Windows 8.1 y versiones posteriores**: No disponible<br>- **Windows Phone 8.1 y versiones posteriores**: No disponible |
| **Versión de SO mínima** | - **Android 4.0 y versiones posteriores**: En cuarentena<br>- **Samsung Knox Standard 4.0 y versiones posteriores**: En cuarentena<br>- **Android Enterprise**: En cuarentena<br><br>- **iOS 8.0 y versiones posteriores**: En cuarentena<br>- **macOS 10.11 y versiones posteriores**: En cuarentena<br><br>- **Windows 8.1 y versiones posteriores**: En cuarentena<br>- **Windows Phone 8.1 y versiones posteriores**: En cuarentena |
| **Versión de SO máxima** | - **Android 4.0 y versiones posteriores**: En cuarentena<br>- **Samsung Knox Standard 4.0 y versiones posteriores**: En cuarentena<br>- **Android Enterprise**: En cuarentena<br><br>- **iOS 8.0 y versiones posteriores**: En cuarentena<br>- **macOS 10.11 y versiones posteriores**: En cuarentena<br><br>- **Windows 8.1 y versiones posteriores**: En cuarentena<br>- **Windows Phone 8.1 y versiones posteriores**: En cuarentena |
| **Atestación de estado de Windows** | - **Android 4.0 y versiones posteriores**: No disponible<br>- **Samsung Knox Standard 4.0 y versiones posteriores**: No disponible<br>- **Android Enterprise**: No disponible<br><br>- **iOS 8.0 y versiones posteriores**: No disponible<br>- **macOS 10.11 y versiones posteriores**: No disponible<br><br>- **Windows 10 y Windows 10 Mobile**: En cuarentena<br>- **Windows 8.1 y versiones posteriores**: En cuarentena<br>- **Windows Phone 8.1 y versiones posteriores**: No disponible |

---------------------------

## <a name="next-steps"></a>Pasos siguientes

- [Configurar ubicaciones](../protect/use-network-locations.md) para su uso con dispositivos Android
- [Crear e implementar directivas](../protect/create-compliance-policy.md) y revisar los requisitos previos
- [Supervisar el cumplimiento del dispositivo](../protect/compliance-policy-monitor.md)
- [Preguntas comunes, problemas y su solución con perfiles y directivas de dispositivos en Microsoft Intune](../configuration/device-profile-troubleshoot.md)
- En [Referencia de entidades de directivas](../developer/reports-ref-policy.md) se brinda información sobre las entidades de directivas de almacenamiento de datos de Intune
