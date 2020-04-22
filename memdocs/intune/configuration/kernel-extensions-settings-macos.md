---
title: Configuración de extensiones de kernel de macOS en Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Agregue, configure o cree configuraciones en dispositivos macOS para que usen extensiones de kernel. Asimismo, deje que los usuarios invaliden extensiones aprobadas, permita todas las extensiones de un identificador de equipo concreto o permita extensiones o aplicaciones específicas en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
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
ms.openlocfilehash: 2e18fad8f1112681a62bcdacd63c652cfd4ad3ac
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359285"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>Ajustes de dispositivos macOS para configurar y usar extensiones de kernel en Intune

En este artículo se enumeran y describen los diferentes valores de configuración de la extensión kernel que se pueden controlar en los dispositivos macOS. Como parte de su solución de administración de dispositivos móviles (MDM), use esta configuración para agregar y administrar extensiones de kernel en sus dispositivos.

Para obtener más información sobre las extensiones de kernel en Intune y conocer los requisitos previos, vea [Incorporación de extensiones de kernel de macOS](kernel-extensions-overview-macos.md).

Estos valores se agregan a un perfil de configuración de dispositivo en Intune y luego se asignan o implementan en los dispositivos macOS.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de extensiones de kernel de dispositivo](kernel-extensions-overview-macos.md).

> [!NOTE]
> Esta configuración se aplica a diferentes tipos de inscripción. Para más información sobre los diferentes tipos de inscripción, consulte [Inscripción en macOS](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Extensiones de kernel

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivo aprobada y automatizada por el usuario

- **Permitir invalidaciones de usuario**: use la opción **Permitir** para que los usuarios puedan aprobar extensiones de kernel no incluidas en el perfil de configuración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que los usuarios permitan extensiones no incluidas en el perfil de configuración. es decir, solo se permiten las extensiones incluidas en el perfil de configuración.

  Vea [Carga de extensiones de kernel aprobadas por el usuario](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (se abre el sitio web de Apple) para obtener más información sobre esta característica.

- **Identificadores de equipo permitidos**: use esta opción para permitir uno o varios identificadores de equipo. Todas las extensiones de kernel firmadas con los identificadores de equipo que se especifiquen estarán permitidas y serán de confianza. En otras palabras, use esta opción para permitir todas las extensiones de kernel incluidas dentro del mismo identificador de equipo, que puede pertenecer a un desarrollador o a un asociado específico.

  **Agregue** un identificador de equipo de extensiones de kernel válidas y firmadas que quiera cargar. Se pueden agregar varios identificadores de equipo. El identificador de equipo debe ser alfanumérico (letras y números) y tener 10 caracteres. Por ejemplo, escriba `ABCDE12345`.

  Después de agregar un identificador de equipo, este también se puede eliminar.

  En el vínculo [Localizar su identificador de equipo](https://help.apple.com/developer-account/#/dev55c3c710c) (se abre el sitio web de Apple) hay más información.

- **Extensiones de kernel permitidas**: use esta configuración para permitir que se puedan abrir sitios web específicos. Solo se permitirán (o serán de confianza) las extensiones de kernel que se especifiquen.

  **Agregue** el identificador de agrupación y el identificador de equipo de una extensión de kernel que quiera cargar. En el caso de las extensiones de kernel heredadas sin firmar, use un identificador de equipo vacío. Se pueden agregar varias extensiones de kernel. El identificador de equipo debe ser alfanumérico (letras y números) y tener 10 caracteres. Por ejemplo, escriba `com.contoso.appname.macos` en **Id. de agrupación** y `ABCDE12345` en **Identificador de equipo**.

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

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).
