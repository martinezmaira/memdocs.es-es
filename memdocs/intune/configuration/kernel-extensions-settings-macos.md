---
title: 'Configuración de la extensión macOS en Microsoft Intune: Azure | Microsoft Docs'
titleSuffix: ''
description: Agregue, configure o cree configuraciones en dispositivos macOS para que usen extensiones del sistema y de kernel. Asimismo, deje que los usuarios invaliden extensiones aprobadas, permita todas las extensiones de un identificador de equipo concreto o permita extensiones o aplicaciones específicas en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b716a7e85f817e95a9f1fec992458e052570d81
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429511"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>Ajustes de dispositivos macOS para configurar y usar extensiones de kernel y del sistema en Intune

> [!NOTE]
> Las extensiones de kernel de macOS se van a reemplazar por extensiones del sistema. Para obtener más información, vea [Sugerencia de soporte técnico: Uso de extensiones del sistema en lugar de extensiones de kernel para macOS Catalina 10.15 en Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

En este artículo se enumeran y describen los diferentes valores de configuración de la extensión de kernel y del sistema que se pueden controlar en los dispositivos macOS. Como parte de su solución de administración de dispositivos móviles (MDM), use esta configuración para agregar y administrar extensiones en sus dispositivos.

Para obtener más información sobre las extensiones en Intune y conocer los requisitos previos, vea [Incorporación de extensiones de macOS](kernel-extensions-overview-macos.md).

Estos valores se agregan a un perfil de configuración de dispositivo en Intune y luego se asignan o implementan en los dispositivos macOS.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de extensiones de macOS](kernel-extensions-overview-macos.md).

> [!NOTE]
> Esta configuración se aplica a diferentes tipos de inscripción. Para más información sobre los diferentes tipos de inscripción, consulte [Inscripción en macOS](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Extensiones de kernel

Esta característica se aplica a:

- macOS 10.13.2 y versiones más recientes.
- Se requiere la inscripción del dispositivo aprobada por el usuario. 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Las opciones se aplican a: inscripción de dispositivos aprobada por el usuario e inscripción de dispositivos automatizada

- **Permitir invalidaciones de usuario**: la opción **Sí** permite a los usuarios aprobar extensiones de kernel no incluidas en el perfil de configuración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que los usuarios permitan extensiones no incluidas en el perfil de configuración. es decir, solo se permiten las extensiones incluidas en el perfil de configuración.

  Vea [Carga de extensiones de kernel aprobadas por el usuario](https://developer.apple.com/library/archive/technotes/tn2459/_index.html), disponible en el sitio web de Apple, para obtener más información sobre esta característica.

- **Identificadores de equipo permitidos**: use esta opción para permitir uno o varios identificadores de equipo. Todas las extensiones de kernel firmadas con los identificadores de equipo que se especifiquen estarán permitidas y serán de confianza. En otras palabras, use esta opción para permitir todas las extensiones de kernel incluidas dentro del mismo identificador de equipo, que puede pertenecer a un desarrollador o a un asociado específico.

  **Agregue** un identificador de equipo de extensiones de kernel válidas y firmadas que se vaya a cargar. Se pueden agregar varios identificadores de equipo. El identificador de equipo debe ser alfanumérico (letras y números) y tener 10 caracteres. Por ejemplo, escriba `ABCDE12345`.

  Después de agregar un identificador de equipo, este también se puede eliminar.

  En el vínculo [Localizar su identificador de equipo](https://help.apple.com/developer-account/#/dev55c3c710c) (se abre el sitio web de Apple) hay más información.

- **Extensiones de kernel permitidas**: use esta configuración para permitir que se puedan abrir sitios web específicos. Solo se permitirán (o serán de confianza) las extensiones de kernel que se especifiquen.

  **Agregue** el identificador de agrupación y el identificador de equipo de una extensión de kernel que se vaya a cargar. En el caso de las extensiones de kernel heredadas sin firmar, use un identificador de equipo vacío. Se pueden agregar varias extensiones de kernel. El identificador de equipo debe ser alfanumérico (letras y números) y tener 10 caracteres. Por ejemplo, escriba `com.contoso.appname.macos` en **Id. de agrupación** y `ABCDE12345` en **Identificador de equipo**.

  > [!TIP]
  > Para obtener el identificador de agrupación de una extensión de kernel (Kext) en un dispositivo macOS, puede hacer lo siguiente:
  >
  > 1. En el terminal, ejecute `kextstat | grep -v com.apple` y anote el resultado. Instale el software o Kext que quiera. Vuelva a ejecutar `kextstat | grep -v com.apple` y busque los cambios.
  >
  >    En el terminal, `kextstat` muestra todas las extensiones de kernel del sistema operativo. 
  >
  > 2. En el dispositivo, abra el archivo de lista de propiedades de información (Info.plist) de un Kext. Se muestra el identificador de agrupación. Cada Kext guarda en su interior un archivo Info.plist.

> [!NOTE]
> No hay que agregar identificadores de equipo ni extensiones de kernel. Puede configurar o lo uno o lo otro.

## <a name="system-extensions"></a>Extensiones del sistema

Esta característica se aplica a:

- macOS 10.15 y versiones más recientes
- Se requiere la inscripción del dispositivo aprobada por el usuario.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Las opciones se aplican a: inscripción de dispositivos aprobada por el usuario e inscripción de dispositivos automatizada

- **Bloquear las invalidaciones del usuario**: la opción **Sí** impide que los usuarios aprueben extensiones del sistema que no estén en la lista de permitidos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios aprueben extensiones desconocidas no incluidas en el perfil de configuración. Es decir, se permiten las extensiones no incluidas en el perfil de configuración.

- **Identificadores de equipo permitidos**: use esta opción para permitir uno o varios identificadores de equipo. Todas las extensiones del sistema firmadas con los id. de equipo que se especifiquen siempre están permitidas y son de confianza. En otras palabras, use esta opción para permitir todas las extensiones del sistema incluidas dentro del mismo id. de equipo, que puede pertenecer a un desarrollador o a un asociado específico.

  **Agregue** un **identificador de equipo** de extensiones del sistema válidas y firmadas que se vaya a cargar. Se pueden agregar varios identificadores de equipo. El identificador de equipo debe ser alfanumérico (letras y números) y tener 10 caracteres. Por ejemplo, escriba `ABCDE12345`.

  Después de agregar un identificador de equipo, este también se puede eliminar.

  En el vínculo [Localizar su identificador de equipo](https://help.apple.com/developer-account/#/dev55c3c710c) (se abre el sitio web de Apple) hay más información.

- **Extensiones del sistema permitidas**: use esta configuración para permitir siempre las extensiones específicas del sistema. Solo se permitirán (o se considerarán de confianza) las extensiones del sistema que se especifiquen.

  **Agregue** el **identificador de agrupación** y el **identificador de equipo** de una extensión del sistema que se vaya a cargar. En el caso de las extensiones del sistema heredadas sin firmar, use un identificador de equipo vacío. Se pueden agregar varias extensiones del sistema. El identificador de equipo debe ser alfanumérico (letras y números) y tener 10 caracteres. Por ejemplo, escriba `com.contoso.appname.macos` en **Id. de agrupación** y `ABCDE12345` en **Identificador de equipo**.

- **Tipos de extensiones del sistema permitidas**: escriba el id. de equipo y los tipos de extensión del sistema que se van a permitir para ese id. de equipo:
  - **Identificador de equipo**: escriba el id. de equipo de otra extensión del sistema que quiera que permita tipos de extensión específicos. También puede escribir un id. de equipo que haya agregado a **Extensiones del sistema permitidas**.
  - **Tipos de extensiones del sistema permitidas**: seleccione los tipos de extensión del sistema que se van a permitir para cada id. de equipo. Las opciones son:
    - Seleccionar todo
    - Extensiones de controlador
    - Extensiones de red
    - Extensiones de seguridad del punto de conexión

    Para obtener más información sobre estos tipos de extensiones, vea [Extensiones del sistema](https://developer.apple.com/system-extensions/), disponible en el sitio web de Apple.

    Puede agregar un id. de equipo de la lista **Extensiones del sistema permitidas** y permitir un tipo de extensión específico. Si la extensión es un tipo que no está permitido, es posible que la extensión no se ejecute.

    Para permitir todos los tipos de extensión de un id. de equipo, agregue este id. a la lista **Extensiones del sistema permitidas**. No agregue el id. de equipo a la lista **Tipos de extensión del sistema permitidos**. En otras palabras, si un id. de equipo está en la lista **Extensiones del sistema permitidas** y no en la lista **Tipos de extensión del sistema permitidos**, se permiten todos los tipos de extensión para ese id. de equipo.

> [!NOTE]
> Agregar el mismo id. de equipo para **Extensiones del sistema permitidas** e **Identificadores de equipo permitidos** puede provocar un error y que el perfil sea incorrecto. No agregue exactamente el mismo identificador de equipo a ambos valores de configuración. 

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).
