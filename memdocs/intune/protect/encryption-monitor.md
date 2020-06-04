---
title: Informe de cifrado para dispositivos cifrados en Microsoft Intune
titleSuffix: Microsoft Intune
description: Vea un informe sobre el estado de cifrado del dispositivo iOS/iPadOS o Windows, y acceda a las claves de recuperación de BitLocker y FileVault desde el portal de Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 1199c6db96325a103394cfb53a4ca70092cd3767
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989654"
---
# <a name="monitor-device-encryption-with-intune"></a>Supervisión del cifrado de dispositivos con Intune

El informe de cifrado de Microsoft Intune es una ubicación centralizada para ver los detalles sobre el estado de cifrado de un dispositivo y buscar opciones para administrar las claves de recuperación del mismo. Las opciones de clave de recuperación disponibles dependen del tipo de dispositivo que se está viendo.

Para buscar el informe, inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Seleccione **Dispositivos** > **Supervisar** y, en *Configuración*, seleccione **Informe de cifrado**.

## <a name="view-encryption-details"></a>Visualización de detalles de cifrado

El informe de cifrado muestra detalles comunes en los dispositivos compatibles que se administran. En las secciones siguientes se proporcionan detalles sobre la información que Intune presenta en el informe.

### <a name="prerequisites"></a>Requisitos previos

El informe de cifrado admite la generación de informes en los dispositivos que ejecutan las versiones siguientes de sistema operativo:

- macOS 10.13 o posterior
- Windows, versión 1607 o posterior

### <a name="report-details"></a>Detalles del informe

En el panel de informe de cifrado se muestra una lista de los dispositivos que se administran con detalles de alto nivel sobre dichos dispositivos. Puede seleccionar un dispositivo de la lista para profundizar y ver detalles adicionales en el panel [Estado de cifrado del dispositivo](#device-encryption-status).

- **Nombre de dispositivo**: representa el nombre del dispositivo.
- **SO**: contiene la plataforma del dispositivo, como Windows o macOS.
- **Versión del SO**: versión de Windows o macOS del dispositivo.
- **Versión de TPM** *(se aplica solo a Windows 10)* : versión del chip del Módulo de plataforma segura (TPM) en el dispositivo Windows 10.
- **Preparación del cifrado**: evaluación de la preparación de los dispositivos para admitir una tecnología de cifrado aplicable, como el cifrado de BitLocker o FileVault. Los dispositivos se identifican de la siguiente manera:
  - **Listo**: el dispositivo se puede cifrar mediante el uso de la directiva MDM, que necesita que el dispositivo cumpla los requisitos siguientes:

    **Para dispositivos macOS**:
    - macOS 10.13 o versiones posteriores

    **Para dispositivos Windows 10**:
    - versión 1709 o posterior de *Business*, *Enterprise*, *Education*, o versión 1809 o posterior de *Pro*.
    - El dispositivo debe tener un chip TPM.

    Para más información, vea el [proveedor de servicios de configuración (CSP) de BitLocker](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) en la documentación de Windows.

  - **No está listo**: El dispositivo no tiene capacidades de cifrado completo, pero admite el cifrado. Por ejemplo, un dispositivo Windows lo podría cifrar un usuario de forma manual o también a través de la directiva de grupo que se puede establecer para permitir el cifrado sin TMP.
  - **No aplicable**: no hay suficiente información para clasificar este dispositivo.

- **Estado de cifrado**: indica si la unidad del sistema operativo está cifrada.

- **Nombre principal del usuario**: usuario primario del dispositivo.

### <a name="device-encryption-status"></a>Estado de cifrado del dispositivo

Cuando se selecciona un dispositivo desde el informe de cifrado, Intune muestra el panel **Estado de cifrado del dispositivo**. Este panel proporciona los siguientes detalles:

- **Nombre de dispositivo**: contiene el nombre del dispositivo que está visualizando.

- **Preparación de cifrado**: evaluación de la preparación de los dispositivos para admitir el cifrado a través de la directiva MDM.

  Por ejemplo: cuando un dispositivo Windows 10 tiene una preparación de *No está listo*, es posible que aún sea compatible con el cifrado. Para que el dispositivo Windows 10 tenga la designación de *Listo*, debe contar con un chip TPM. No es necesario que los chips TPM sean compatibles con el cifrado. (Para obtener más información, consulte *Preparación de cifrado* en la sección anterior).

- **Estado de cifrado**: indica si la unidad del sistema operativo está cifrada. Intune puede tardar hasta 24 horas en generar informes sobre el estado de cifrado de un dispositivo o un cambio de ese estado. En este tiempo se incluye el tiempo de cifrado del sistema operativo, así como el tiempo necesario para que el dispositivo informe a Intune.

  Para acelerar la generación de informes del estado de cifrado de FileVault antes de que se produzca el registro del dispositivo con normalidad, haga que los usuarios sincronicen sus dispositivos una vez completado el cifrado.

- **Perfiles**: una lista de los perfiles de *Configuración del dispositivo* que se aplican a este dispositivo y que se configuran con los valores siguientes:

  - macOS:
    - Tipo de perfil = *Endpoint Protection*
    - Configuración > FileVault > FileVault = *Habilitar*

  - Windows 10:
    - Tipo de perfil = *Endpoint Protection*
    - Configuración > Cifrado de Windows > Cifrar dispositivos = *necesario*

  Se puede usar esta lista de perfiles con el fin de identificar directivas individuales para revisarlas en caso de que el *resumen de estado del perfil* indique problemas.

- **Resumen de estado de perfil**: resumen de los perfiles que se aplican a este dispositivo. El resumen representa la condición menos favorable entre los perfiles aplicables. Por ejemplo, aunque solo se produzca un error en un perfil aplicable de entre varios, el *resumen de estado de perfil* mostrará *Error*.

  Para ver más detalles de un estado, vaya a **Intune** > **Configuración del dispositivo** > **Perfiles** y seleccione el perfil. Opcionalmente, seleccione **Estado del dispositivo** y, a continuación, seleccione un dispositivo.

- **Detalles del estado**: detalles avanzados sobre el estado de cifrado del dispositivo.

  > [!IMPORTANT]
  > En dispositivos Windows 10, Intune solo muestra *Detalles del estado* para dispositivos que ejecutan la *actualización de Windows 10 de abril de 2019* o una versión posterior.

  Este campo muestra la información de cada error aplicable que se puede detectar. Puede usar esta información para comprender por qué un dispositivo podría no estar listo para el cifrado.

  Los siguientes son ejemplos de los detalles de estado que se pueden informar en Intune:

  **macOS**:
  - La clave de recuperación todavía no se ha recuperado ni almacenado. Lo más probable es que el dispositivo no se haya desbloqueado o que no se haya protegido.

    *Tenga en cuenta lo siguiente: este resultado no representa necesariamente una condición de error, sino un estado temporal que podría deberse a un momento en el dispositivo en el que se debe configurar la custodia de las claves de recuperación antes de que se envíe la solicitud de cifrado al dispositivo. Este estado también puede indicar que el dispositivo permanece bloqueado o no se ha registrado con Intune recientemente. Por último, dado que el cifrado de FileVault no se inicia hasta que un dispositivo está conectado (en carga), es posible que un usuario reciba una clave de recuperación para un dispositivo que todavía no esté cifrado*.

  - El usuario está aplazando el cifrado o actualmente se encuentra en el proceso de cifrado.

    *Tenga en cuenta lo siguiente: o el usuario todavía no ha cerrado sesión después de recibir la solicitud de cifrado, lo cual es necesario para que FileVault pueda cifrar el dispositivo, o bien ha descifrado manualmente el dispositivo. Intune no puede impedir que un usuario descifre su dispositivo.*

  - El dispositivo ya está cifrado. El usuario del dispositivo debe descifrar el dispositivo para continuar.

    *Tenga en cuenta lo siguiente: Intune no puede configurar FileVault en un dispositivo que ya está cifrado. En lugar de eso, el usuario debe descifrar de forma manual el dispositivo antes de que se pueda administrar mediante una directiva de configuración de dispositivo e Intune.*

  - FileVault necesita que el usuario apruebe su perfil de administración en macOS Catalina y versiones posteriores.

    *Tenga en cuenta lo siguiente: a partir de la versión de macOS 10.15 (Catalina), la configuración de inscripción aprobada por el usuario puede tener como resultado un requisito por el que los usuarios deban aprobar el cifrado de FileVault de forma manual. Para obtener más información, en la documentación de Intune consulte [Inscripción aprobada por el usuario](../enrollment/macos-enroll.md)* .

  - Desconocido.

    *Tenga en cuenta lo siguiente: Una posible causa de un estado desconocido es que el dispositivo está bloqueado e Intune no puede iniciar el proceso de custodia o de cifrado. Una vez desbloqueado el dispositivo, el progreso puede continuar*.

  **Windows 10**:
  - La directiva de BitLocker requiere el consentimiento del usuario para iniciar el Asistente para Cifrado de unidad BitLocker con el fin de iniciar el cifrado del volumen del sistema operativo, pero el usuario no ha dado su consentimiento.

  - El método de cifrado del volumen del sistema operativo no coincide con la directiva de BitLocker.

  - La directiva de BitLocker requiere protección con TPM para el volumen del sistema operativo, pero no se utiliza TPM.

  - La directiva de BitLocker requiere protección solo con TPM para el volumen del sistema operativo, pero no se utiliza protección con TPM.

  - La directiva de BitLocker requiere protección con TPM y PIN para el volumen del sistema operativo, pero no se utiliza protección con TPM y PIN.

  - La directiva de BitLocker requiere protección con TPM y PIN para el volumen del sistema operativo, pero no se usa protección con TPM y PIN.

  - La directiva de BitLocker requiere protección con TPM, PIN y clave de inicio para el volumen del sistema operativo, pero no se utiliza protección con TPM, PIN y clave de inicio.

  - El volumen del sistema operativo no está protegido.

  - Error de copia de seguridad de la clave de recuperación.

  - Una unidad de disco fija no está protegida.

  - El método de cifrado de la unidad de disco fija no coincide con la directiva de BitLocker.

  - Para cifrar unidades, la directiva de BitLocker requiere que el usuario inicie sesión como administrador, o bien, si el dispositivo está unido a Azure AD, debe establecerse la directiva AllowStandardUserEncryption en 1.

  - Entorno de recuperación de Windows (WinRE) no está configurado.

  - No hay un TPM disponible para BitLocker, bien porque no existe, porque se ha deshabilitado en el registro o porque el sistema operativo está en una unidad extraíble.

  - El TPM no está listo para BitLocker.

  - La red no está disponible y es necesaria para la copia de seguridad de clave de recuperación.

## <a name="export-report-details"></a>Exportación de detalles del informe

Mientras ve el panel de informe de cifrado, puede seleccionar **Exportar** para crear una descarga de archivo *.csv* de los detalles del informe. Este informe incluye los detalles de alto nivel del panel *Informe de cifrado* y los detalles del *Estado de cifrado* para cada dispositivo que administra.

![Exportación de detalles](./media/encryption-monitor/export.png)

Este informe se puede usar para identificar problemas en grupos de dispositivos. Por ejemplo, podría usar el informe para identificar una lista de todos los dispositivos macOS que informen *El usuario ya ha habilitado FileVault*, lo que indica qué dispositivos deben descifrarse de forma manual antes de que Intune pueda empezar a administrar su configuración de FileVault.

## <a name="manage-recovery-keys"></a>Administración de claves de recuperación

Para obtener detalles sobre la administración de claves de recuperación, vea lo siguiente en la documentación de Intune:

FileVault de macOS:
- [Recuperación de clave de recuperación personal](../protect/encrypt-devices-filevault.md#retrieve-personal-recovery-key)
- [Giro de claves de recuperación](../protect/encrypt-devices-filevault.md#rotate-recovery-keys)
- [Recuperación de claves de recuperación](../protect/encrypt-devices-filevault.md#recover-recovery-keys)

BitLocker de Windows 10:
- [Giro de claves de recuperación de BitLocker](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)

## <a name="next-steps"></a>Pasos siguientes

[Administración de directiva de BitLocker](../protect/encrypt-devices.md)

[Administración de directiva de FileVault](encrypt-devices-filevault.md)
