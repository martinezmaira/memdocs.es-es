---
title: 'Restricciones de dispositivos Windows 10 Team de Surface Hub en Microsoft Intune: Azure | Microsoft Docs'
titleSuffix: ''
description: Use Intune para agregar o configurar valores de dispositivos de Surface Hub que ejecutan Windows 10 Team.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429688"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Configuración de Windows 10 Team para permitir o restringir características en dispositivos de Surface Hub con Intune

En este artículo, se muestran las opciones de configuración de restricciones de dispositivos de Microsoft Intune que puede configurar para los dispositivos que ejecutan Windows 10 Team, como los dispositivos de Surface Hub.

## <a name="before-you-begin"></a>Antes de comenzar

[Creación del perfil de dispositivo](device-restrictions-configure.md#create-the-profile).

## <a name="apps-and-experience"></a>Aplicaciones y experiencia

Esta configuración usa el [CSP de SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Reactivar pantalla cuando hay alguien en la sala**: **Bloquear** impide que la pantalla se reactive automáticamente cuando su sensor detecta alguien en la sala. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Información sobre la reunión en la pantalla de inicio de sesión**: elija la información que se muestra en el icono de reuniones de la pantalla de inicio de sesión. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Solo el organizador y la hora**
  - **Organizador, hora y asunto (asunto oculto para las reuniones privadas)**
- **URL de imagen de fondo de pantalla de inicio de sesión**: Escriba la dirección URL de una imagen .png que quiera usar como fondo personalizado en la pantalla de **inicio de sesión** en los dispositivos de Windows 10 Team. La imagen debe estar en formato PNG y la dirección URL debe comenzar con `https://`.
- **Iniciar automáticamente la aplicación Conectar**: **Bloquear** impide que la aplicación Conectar se abra automáticamente cuando se inicia una proyección. Si se bloquea, los usuarios pueden iniciar manualmente la aplicación Conectar desde la configuración del centro. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Sugerencias de inicio de sesión**: **Bloquear** deshabilita el relleno automático del cuadro de diálogo de inicio de sesión con invitados de reuniones programadas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Mis reuniones y archivos**: **Bloquear** deshabilita la característica **Mis reuniones y archivos** en el menú Inicio. Esta característica muestra las reuniones y los archivos del usuario con sesión iniciada de Office 365. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Azure Operational Insights**: **Habilitar** recopila, almacena y analiza los datos de registro de los dispositivos de Windows 10 Team con Azure Operational Insights. Azure Operational Insights forma parte del conjunto de Microsoft Operations Manager. Para conectarse a **Azure Operational Insights**, especifique el **identificador del área de trabajo** y una clave del área de trabajo.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no recopilar estos datos.

## <a name="maintenance"></a>Mantenimiento

Esta configuración usa el [CSP de SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Período de mantenimiento para actualizaciones**: **Habilitar** crea un período de mantenimiento cuando se pueden instalar actualizaciones. Especifique la **Hora de inicio** y la **Duración en horas** (de 1-5 horas) del período de mantenimiento.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="session"></a>Sesión

Esta configuración usa el [CSP de SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Volumen**: Escriba el valor de volumen predeterminado de una nueva sesión (de 0-100). Cuando se deja en blanco, Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría establecer el volumen en 45.
- **Tiempo de espera de la pantalla**: Especifique el número de minutos hasta que la pantalla Concentrador se apaga.
- **Tiempo de espera de sesión**: Especifica el número de minutos hasta que se agota el tiempo de espera de la sesión.
- **Tiempo de espera en suspensión**: Especifique el número de minutos hasta que el Concentrador entra en modo de suspensión.
- **Reanudación de la sesión**: **Bloquear** impide que los usuarios reanuden una sesión cuando se agota el tiempo de espera de la sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="wireless-projection"></a>Proyección inalámbrica

Esta configuración usa el [CSP de SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **PIN para proyección inalámbrica**: **Requerir** obliga a los usuarios a escribir un PIN antes de usar las características de proyección inalámbrica en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Proyección inalámbrica de Miracast**: **Bloquear** impide el uso de dispositivos habilitados para Miracast en el proyecto. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Canal de proyección inalámbrica de Miracast**: Seleccione el canal de Miracast para establecer la conexión.

## <a name="next-steps"></a>Pasos siguientes

Para más información, consulte [Configuración de restricciones de dispositivos en Microsoft Intune](device-restrictions-configure.md).

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).
