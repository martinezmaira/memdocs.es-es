---
title: 'Agregar una configuración personalizada para dispositivos Windows Phone 8.1 en Microsoft Intune: Azure | Microsoft Docs'
titleSuffix: ''
description: Agregue o cree un perfil personalizado para usar la configuración OMA-URI para dispositivos con Windows Phone 8.1 en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce8433ee87c0f5e4b397003b78c0ceb751eb46b7
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556275"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Usar una configuración personalizada para dispositivos Windows Phone 8.1 en Intune

Con Microsoft Intune, puede agregar o crear una configuración personalizada para los dispositivos Windows Phone 8.1 mediante "perfiles personalizados". Los perfiles personalizados son una característica de Intune diseñada para agregar una configuración de dispositivo y características que no están integradas Intune.

Los perfiles personalizados de Windows Phone 8.1 usan la configuración OMA-URI (identificador uniforme de recursos de Open Mobile Alliance) para configurar diferentes características. Esta configuración la suelen usar los fabricantes de dispositivos móviles para controlar las características en el dispositivo. En la [documentación del protocolo de MDM de Windows Phone 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) se muestra la configuración.

En este artículo se muestra cómo crear un perfil personalizado para dispositivos Windows Phone 8.1. 

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de correo electrónico de Windows Phone 8.1](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Configuración de OMA-URI personalizada

- **Configuración de OMA-URI**: **Agregue** la configuración siguiente:

  - **Nombre**: Escriba un nombre único para el valor OMA-URI que le ayude a identificarlo en la lista de valores de configuración.
  - **Descripción**: escriba una descripción que proporcione información general sobre el valor y cualquier otra información relevante que ayude a encontrar el perfil.
  - **OMA-URI** (distingue mayúsculas de minúsculas): escriba la configuración OMA-URI que quiere usar.
  - **Tipo de datos**: seleccione el tipo de datos que se va a usar para esta configuración OMA-URI. Las opciones son:

    - String
    - Cadena (archivo XML)
    - Fecha y hora
    - Integer
    - Punto flotante
    - Boolean
    - Base64 (archivo)

  - **Valor**: escriba el valor de datos que quiere asociar con la configuración OMA-URI especificada. El valor depende del tipo de datos que ha seleccionado. Por ejemplo, si selecciona **Fecha y hora**, seleccione el valor en un selector de fecha.

  Después de agregar algunos valores de configuración, puede seleccionar **Exportar**. Haga clic en **Exportar** para crear una lista de todos los valores agregados en un archivo de valores separados por comas (.csv).

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, los dispositivos telefónicos Windows 8.1 no pueden cambiar de red móvil cuando se viaja fuera del área de cobertura del operador.

- **Nombre**: permita la itinerancia de datos móviles.
- **Descripción**: permita o no la itinerancia de datos móviles.
- **OMA-URI** (distingue mayúsculas de minúsculas): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Tipo de datos**: Integer
- **Valor**: 0

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

Cree un [perfil personalizado en dispositivos Windows 10](custom-settings-windows-10.md).
