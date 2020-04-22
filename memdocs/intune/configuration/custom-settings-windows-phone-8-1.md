---
title: 'Agregar una configuración personalizada para dispositivos Windows Phone 8.1 en Microsoft Intune: Azure | Microsoft Docs'
titleSuffix: ''
description: Agregue o cree un perfil personalizado para usar la configuración OMA-URI para dispositivos con Windows Phone 8.1 en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1bea9047d65faf449c77e1a677000d32e883a76
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "79364531"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Usar una configuración personalizada para dispositivos Windows Phone 8.1 en Intune

Con Microsoft Intune, puede agregar o crear una configuración personalizada para los dispositivos Windows Phone 8.1 mediante "perfiles personalizados". Los perfiles personalizados son una característica de Intune diseñada para agregar una configuración de dispositivo y características que no están integradas Intune.

Los perfiles personalizados de Windows Phone 8.1 usan la configuración OMA-URI (identificador uniforme de recursos de Open Mobile Alliance) para configurar diferentes características. Esta configuración la suelen usar los fabricantes de dispositivos móviles para controlar las características en el dispositivo. En la [documentación del protocolo de MDM de Windows Phone 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) se muestra la configuración.

En este artículo se muestra cómo crear un perfil personalizado para dispositivos Windows Phone 8.1. 

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba los valores siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un nombre de perfil válido es **Perfil personalizado de Windows Phone**.
    - **Descripción**: escriba una descripción con información general sobre la configuración y otros detalles importantes.
    - **Plataforma**: Seleccione **Windows Phone 8.1**.
    - **Tipo de perfil**: seleccione **Personalizado**.

4. En **Configuración OMA-URI personalizada**, seleccione **Agregar**. Escriba los valores siguientes:

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

5. Haga clic en **Aceptar** para guardar los cambios. Continúe agregando más valores según sea necesario.
6. Cuando termine, seleccione **Aceptar** > **Crear** para crear el perfil de Intune. Una vez hecho, el perfil aparece en la lista **Dispositivos - Perfiles de configuración**.

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, los dispositivos telefónicos Windows 8.1 no pueden cambiar de red móvil cuando se viaja fuera del área de cobertura del operador.

- **Nombre**: permita la itinerancia de datos móviles.
- **Descripción**: permita o no la itinerancia de datos móviles.
- **OMA-URI** (distingue mayúsculas de minúsculas): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Tipo de datos**: Integer
- **Valor**: 0

## <a name="next-steps"></a>Pasos siguientes

Se crea el perfil, pero todavía no hace nada. Después, [asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

Cree un [perfil personalizado en dispositivos Windows 10](custom-settings-windows-10.md).
