---
title: 'Agregar una configuración personalizada para dispositivos Windows 10 en Microsoft Intune: Azure | Microsoft Docs'
description: Agregue o cree un perfil personalizado para usar la configuración OMA-URI para dispositivos con Windows 10 en Microsoft Intune. Use un perfil personalizado para agregar una configuración personalizada.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96074f4bea22b7468b1f210d631f0912eeafe7b5
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428986"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Usar una configuración personalizada para dispositivos Windows 10 en Intune

En este artículo se enumeran y describen todas las diferentes opciones personalizadas que se pueden controlar en los dispositivos con Windows 10 y versiones posteriores. Como parte de su solución de administración de dispositivos móviles (MDM), use estas opciones para definir configuraciones que no estén integradas en Intune.

Para obtener más información sobre los perfiles personalizados, vea [Crear un perfil con una configuración personalizada en Intune](custom-settings-configure.md).

Estos valores se agregan a un perfil de configuración de dispositivo en Intune y luego se asignan o implementan en los dispositivos con Windows 10.

Esta característica se aplica a:

- Windows 10 y versiones posteriores

Los perfiles personalizados de Windows 10 usan la configuración OMA-URI (identificador uniforme de recursos de Open Mobile Alliance) para configurar diferentes características. Esta configuración la suelen usar los fabricantes de dispositivos móviles para controlar las características en el dispositivo.

Windows 10 tiene disponibles muchos valores de proveedores de servicios de configuración (CSP), como el [proveedor de servicios de configuración de directivas (CSP de directivas)](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers).

Si busca una configuración determinada, recuerde que el [perfil de restricción de dispositivos de Windows 10](device-restrictions-windows-10.md) incluye muchas configuraciones integradas. Por lo tanto, es posible que no necesite especificar valores personalizados.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil personalizado de Windows 10](custom-settings-configure.md#create-the-profile).

## <a name="oma-uri-settings"></a>Configuración de OMA-URI

**Agregar**: Escriba los valores siguientes:

- **Nombre**: Escriba un nombre único para el valor OMA-URI que le ayude a identificarlo en la lista de valores de configuración.
- **Descripción**: escriba una descripción con información general sobre la configuración y otros detalles importantes.
- **OMA-URI** (distingue mayúsculas de minúsculas): escriba la configuración OMA-URI que quiere usar.
- **Tipo de datos**: seleccione el tipo de datos que se va a usar para esta configuración OMA-URI. Las opciones son:

  - Base64 (archivo)
  - Boolean
  - Cadena (archivo XML)
  - Fecha y hora
  - String
  - Punto flotante
  - Integer

- **Valor**: escriba el valor de datos que quiere asociar con la configuración OMA-URI especificada. El valor depende del tipo de datos que ha seleccionado. Por ejemplo, si selecciona **Fecha y hora**, seleccione el valor en un selector de fecha.

Después de agregar algunos valores de configuración, puede seleccionar **Exportar**. Haga clic en **Exportar** para crear una lista de todos los valores agregados en un archivo de valores separados por comas (.csv).

## <a name="find-the-policies-you-can-configure"></a>Buscar las directivas que se pueden configurar

Encontrará una lista completa de todos los proveedores de servicio de configuración (CSP) que Windows 10 admite en la [referencia del proveedor de servicios de configuración](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference).

No todas las configuraciones son compatibles con todas las versiones de Windows 10. En la [referencia del proveedor de servicios de configuración](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) se indica qué versiones son compatibles con cada CSP.

Además, Intune no es compatible con todas las configuraciones que aparecen en la [referencia del proveedor de servicios de configuración](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference). Para saber si Intune admite la configuración que quiere, abra el artículo correspondiente a dicha configuración. En la página de cada configuración se muestra la operación que admite. Para trabajar con Intune, la configuración debe ser compatible con las operaciones **Add**, **Replace** y **Get**. Si el valor devuelto por la operación **Get** no coincide con el proporcionado por las operaciones **Add** o **Replace**, Intune notifica un error de cumplimiento.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

[Más información sobre los perfiles personalizados de Intune](custom-settings-configure.md).
